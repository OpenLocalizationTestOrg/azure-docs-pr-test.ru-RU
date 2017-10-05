---
title: "<span data-ttu-id=\"0fc61-101\">Удаленное управление службой в Service Fabric | Документация Майкрософт</span><span class=\"sxs-lookup\"><span data-stu-id=\"0fc61-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"0fc61-102\">Удаленное взаимодействие Service Fabric позволяет осуществлять обмен данными между клиентами и службами с помощью удаленного вызова процедур.</span><span class=\"sxs-lookup\"><span data-stu-id=\"0fc61-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="0fc61-103">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0fc61-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="0fc61-104">Для служб, которые не привязаны к определенному протоколу обмена данными или стеку, например веб-API, Windows Communication Foundation (WCF) или др., платформа Reliable Services предоставляет механизм удаленного взаимодействия для быстрой и простой настройки удаленного вызова процедур.</span><span class="sxs-lookup"><span data-stu-id="0fc61-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="0fc61-105">Настройка удаленного доступа в службе</span><span class="sxs-lookup"><span data-stu-id="0fc61-105">Set up remoting on a service</span></span>
<span data-ttu-id="0fc61-106">Процесс настройки удаленного доступа для службы состоит из двух простых этапов.</span><span class="sxs-lookup"><span data-stu-id="0fc61-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="0fc61-107">Создание интерфейса для реализации в службе.</span><span class="sxs-lookup"><span data-stu-id="0fc61-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="0fc61-108">Этот интерфейс определяет методы, которые будут доступны для удаленного вызова процедур в службе.</span><span class="sxs-lookup"><span data-stu-id="0fc61-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="0fc61-109">Эти методы должны быть асинхронными методами, возвращающими задачи.</span><span class="sxs-lookup"><span data-stu-id="0fc61-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="0fc61-110">Интерфейс должен реализовать `Microsoft.ServiceFabric.Services.Remoting.IService` , чтобы показать, что служба имеет интерфейс удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="0fc61-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="0fc61-111">Используйте прослушиватель удаленного взаимодействия в службе.</span><span class="sxs-lookup"><span data-stu-id="0fc61-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="0fc61-112">Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="0fc61-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="0fc61-113">Пространство имен `Microsoft.ServiceFabric.Services.Remoting.Runtime` содержит метод расширения `CreateServiceRemotingListener` для служб без отслеживания и с отслеживанием состояния, который можно использовать, чтобы создать прослушиватель удаленного взаимодействия с использованием транспортного протокола удаленного взаимодействия по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0fc61-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="0fc61-114">Примечание. Пространство имен `Remoting` доступно как отдельный пакет NuGet `Microsoft.ServiceFabric.Services.Remoting`.</span><span class="sxs-lookup"><span data-stu-id="0fc61-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="0fc61-115">Например, приведенная ниже служба без отслеживания состояния предоставляет один метод для получения "Hello World" посредством удаленного вызова процедуры.</span><span class="sxs-lookup"><span data-stu-id="0fc61-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="0fc61-116">Аргументы и возвращаемые данные в интерфейсе службы могут иметь простые, сложные или настраиваемые типы, однако они должны быть сериализуемыми с помощью объекта .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fc61-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="0fc61-117">Вызов удаленных методов службы</span><span class="sxs-lookup"><span data-stu-id="0fc61-117">Call remote service methods</span></span>
<span data-ttu-id="0fc61-118">Вызов методов в службе с помощью стека удаленного взаимодействия осуществляется с помощью локального прокси-сервера для службы через класс `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` .</span><span class="sxs-lookup"><span data-stu-id="0fc61-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="0fc61-119">Метод `ServiceProxy` создает локальный прокси-сервер, используя тот же интерфейс, который реализует служба.</span><span class="sxs-lookup"><span data-stu-id="0fc61-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="0fc61-120">С помощью этого прокси можно без труда удаленно вызвать методы в интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="0fc61-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="0fc61-121">Платформа удаленного взаимодействия распространяет исключения, созданные в службе, на клиент.</span><span class="sxs-lookup"><span data-stu-id="0fc61-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="0fc61-122">Поэтому логика обработки исключений на стороне клиента с использованием `ServiceProxy` может напрямую обрабатывать порождаемые службой исключения.</span><span class="sxs-lookup"><span data-stu-id="0fc61-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="0fc61-123">Время существования ServiceProxy</span><span class="sxs-lookup"><span data-stu-id="0fc61-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="0fc61-124">Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно.</span><span class="sxs-lookup"><span data-stu-id="0fc61-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="0fc61-125">Прокси-сервер службы можно использовать повторно, если он нужен пользователю.</span><span class="sxs-lookup"><span data-stu-id="0fc61-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="0fc61-126">Пользователь может повторно использовать один и тот же прокси-сервер при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="0fc61-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="0fc61-127">Каждый ServiceProxy содержит клиент обмена данными, используемый для отправки сообщений по сети.</span><span class="sxs-lookup"><span data-stu-id="0fc61-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="0fc61-128">При вызове API выполняется внутренняя проверка допустимости клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="0fc61-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="0fc61-129">В зависимости от ее результата можно будет повторно создать клиент обмена данными.</span><span class="sxs-lookup"><span data-stu-id="0fc61-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="0fc61-130">Поэтому пользователю не требуется заново создавать ServiceProxy при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="0fc61-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="0fc61-131">Время существования ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="0fc61-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="0fc61-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="0fc61-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="0fc61-133">Если вы используете API ServiceProxy.Create для создания прокси-сервера, то платформа создает одноэлементную ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="0fc61-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="0fc61-134">При необходимости переопределить свойства [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) имеет смысл создать фабрику вручную.</span><span class="sxs-lookup"><span data-stu-id="0fc61-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="0fc61-135">Создание фабрики — ресурсоемкая операция.</span><span class="sxs-lookup"><span data-stu-id="0fc61-135">Factory is an expensive operation.</span></span> <span data-ttu-id="0fc61-136">ServiceProxyFactory хранит кэш клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="0fc61-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="0fc61-137">Рекомендуется кэшировать ServiceProxyFactory на как можно больший период времени.</span><span class="sxs-lookup"><span data-stu-id="0fc61-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="0fc61-138">Обработка исключений удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="0fc61-138">Remoting Exception Handling</span></span>
<span data-ttu-id="0fc61-139">Все исключения удаленного взаимодействия, порождаемые API службы, отправляются обратно в клиент как AggregateException.</span><span class="sxs-lookup"><span data-stu-id="0fc61-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="0fc61-140">Исключения RemoteException должны быть сериализуемыми в формат DataContract, иначе API прокси-сервера получит исключение [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) с ошибкой сериализации.</span><span class="sxs-lookup"><span data-stu-id="0fc61-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="0fc61-141">ServiceProxy обрабатывает все исключения отработки отказа для секции службы, для которого он создан.</span><span class="sxs-lookup"><span data-stu-id="0fc61-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="0fc61-142">Он повторно разрешает конечные точки в случае исключений отработки отказа (повторяющихся исключений) и повторяет вызов к правильной конечной точке.</span><span class="sxs-lookup"><span data-stu-id="0fc61-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="0fc61-143">Число повторных попыток для исключения отработки отказа не ограничено.</span><span class="sxs-lookup"><span data-stu-id="0fc61-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="0fc61-144">В случае исключений TransientException только повторяется попытка вызова.</span><span class="sxs-lookup"><span data-stu-id="0fc61-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="0fc61-145">Параметры повтора по умолчанию определяются [OperationRetrySettings]</span><span class="sxs-lookup"><span data-stu-id="0fc61-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="0fc61-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings). Пользователь может настроить эти значения, передав объект OperationRetrySettings в конструктор ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="0fc61-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc61-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fc61-147">Next steps</span></span>
* [<span data-ttu-id="0fc61-148">Веб-API с OWIN в модели Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0fc61-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="0fc61-149">Взаимодействие WCF с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0fc61-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="0fc61-150">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0fc61-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
