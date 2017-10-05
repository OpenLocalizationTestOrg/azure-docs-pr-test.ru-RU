---
title: "Удаленное управление службой в Azure Service Fabric | Документация Майкрософт"
description: "Удаленное взаимодействие Service Fabric позволяет осуществлять обмен данными между клиентами и службами с помощью удаленного вызова процедур."
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
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="9c1e4-103">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c1e4-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c1e4-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="9c1e4-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="9c1e4-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="9c1e4-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="9c1e4-106">Платформа Reliable Services предоставляет механизм удаленного взаимодействия для быстрой и простой настройки удаленного вызова процедур.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="9c1e4-107">Настройка удаленного доступа в службе</span><span class="sxs-lookup"><span data-stu-id="9c1e4-107">Set up remoting on a service</span></span>
<span data-ttu-id="9c1e4-108">Процесс настройки удаленного доступа для службы состоит из двух простых этапов.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="9c1e4-109">Создание интерфейса для реализации в службе.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="9c1e4-110">Этот интерфейс определяет методы, которые будут доступны для удаленного вызова процедур в службе.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="9c1e4-111">Эти методы должны быть асинхронными методами, возвращающими задачи.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="9c1e4-112">Интерфейс должен реализовать `microsoft.serviceFabric.services.remoting.Service` , чтобы показать, что служба имеет интерфейс удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="9c1e4-113">Используйте прослушиватель удаленного взаимодействия в службе.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="9c1e4-114">Это реализация `CommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="9c1e4-115">`FabricTransportServiceRemotingListener` можно использовать, чтобы создать прослушиватель удаленного взаимодействия с использованием транспортного протокола удаленного взаимодействия по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="9c1e4-116">Например, приведенная ниже служба без отслеживания состояния предоставляет один метод для получения "Hello World" посредством удаленного вызова процедуры.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="9c1e4-117">Аргументы и возвращаемые данные в интерфейсе службы могут иметь простые, сложные или настраиваемые типы, но они должны быть сериализуемыми.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="9c1e4-118">Вызов удаленных методов службы</span><span class="sxs-lookup"><span data-stu-id="9c1e4-118">Call remote service methods</span></span>
<span data-ttu-id="9c1e4-119">Вызов методов в службе с помощью стека удаленного взаимодействия осуществляется с помощью локального прокси-сервера для службы через класс `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` .</span><span class="sxs-lookup"><span data-stu-id="9c1e4-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="9c1e4-120">Метод `ServiceProxyBase` создает локальный прокси-сервер, используя тот же интерфейс, который реализует служба.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="9c1e4-121">С помощью этого прокси можно без труда удаленно вызвать методы в интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="9c1e4-122">Платформа удаленного взаимодействия распространяет исключения, созданные в службе, на клиент.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="9c1e4-123">Поэтому логика обработки исключений на стороне клиента с использованием `ServiceProxyBase` может напрямую обрабатывать порождаемые службой исключения.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="9c1e4-124">Время существования ServiceProxy</span><span class="sxs-lookup"><span data-stu-id="9c1e4-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="9c1e4-125">Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="9c1e4-126">Прокси-сервер службы можно использовать повторно, если он нужен пользователю.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="9c1e4-127">Пользователь может повторно использовать один и тот же прокси-сервер при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="9c1e4-128">Каждый ServiceProxy содержит клиент обмена данными, используемый для отправки сообщений по сети.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="9c1e4-129">При вызове API выполняется внутренняя проверка допустимости клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="9c1e4-130">В зависимости от ее результата можно будет повторно создать клиент обмена данными.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="9c1e4-131">Поэтому пользователю не требуется заново создавать ServiceProxy при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="9c1e4-132">Время существования ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="9c1e4-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="9c1e4-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="9c1e4-134">Если вы используете API `ServiceProxyBase.create` для создания прокси-сервера, то платформа создает `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="9c1e4-135">При необходимости переопределить свойства [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) имеет смысл создать фабрику вручную.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="9c1e4-136">Создание фабрики — ресурсоемкая операция.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-136">Factory is an expensive operation.</span></span> <span data-ttu-id="9c1e4-137">`FabricServiceProxyFactory` хранит кэш клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="9c1e4-138">Рекомендуется кэшировать `FabricServiceProxyFactory` на как можно больший период времени.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="9c1e4-139">Обработка исключений удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="9c1e4-139">Remoting Exception Handling</span></span>
<span data-ttu-id="9c1e4-140">Все исключения удаленного взаимодействия, порождаемые API службы, отправляются обратно в клиент как RuntimeException или FabricException.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="9c1e4-141">ServiceProxy обрабатывает все исключения отработки отказа для секции службы, для которого он создан.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="9c1e4-142">Он повторно разрешает конечные точки в случае исключений отработки отказа (повторяющихся исключений) и повторяет вызов к правильной конечной точке.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="9c1e4-143">Число повторных попыток для исключения отработки отказа не ограничено.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="9c1e4-144">В случае исключений TransientException только повторяется попытка вызова.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="9c1e4-145">Параметры повтора по умолчанию определяются [OperationRetrySettings]</span><span class="sxs-lookup"><span data-stu-id="9c1e4-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="9c1e4-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings). Пользователь может настроить эти значения, передав объект OperationRetrySettings в конструктор ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="9c1e4-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c1e4-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c1e4-147">Next steps</span></span>
* [<span data-ttu-id="9c1e4-148">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c1e4-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
