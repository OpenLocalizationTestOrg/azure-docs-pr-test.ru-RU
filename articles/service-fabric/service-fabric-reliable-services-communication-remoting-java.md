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
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="48558-103">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="48558-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48558-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="48558-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="48558-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="48558-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="48558-106">Платформа надежного обмена Hello предоставляет tooquickly механизм удаленного взаимодействия и легко настроить удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="48558-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="48558-107">Настройка удаленного доступа в службе</span><span class="sxs-lookup"><span data-stu-id="48558-107">Set up remoting on a service</span></span>
<span data-ttu-id="48558-108">Процесс настройки удаленного доступа для службы состоит из двух простых этапов.</span><span class="sxs-lookup"><span data-stu-id="48558-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="48558-109">Создайте интерфейс для tooimplement вашей службы.</span><span class="sxs-lookup"><span data-stu-id="48558-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="48558-110">Этот интерфейс определяет hello методы, которые доступны для удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="48558-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="48558-111">Hello методы должны быть возвращающий задачу асинхронный метод.</span><span class="sxs-lookup"><span data-stu-id="48558-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="48558-112">должен быть реализован интерфейс Hello `microsoft.serviceFabric.services.remoting.Service` toosignal, hello службы имеет интерфейс удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="48558-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="48558-113">Используйте прослушиватель удаленного взаимодействия в службе.</span><span class="sxs-lookup"><span data-stu-id="48558-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="48558-114">Это реализация `CommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="48558-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="48558-115">`FabricTransportServiceRemotingListener`можно использовать toocreate прослушивателя удаленного взаимодействия, используя протокол удаленного доступа по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="48558-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="48558-116">Например hello следующей без сохранения состояния службы предоставляет один метод tooget «Hello World», через удаленный вызов процедуры.</span><span class="sxs-lookup"><span data-stu-id="48558-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="48558-117">аргументы Hello и hello возвращают типы в интерфейс hello службы может быть любой простой, сложных или пользовательских типов, но они должны быть сериализуемыми.</span><span class="sxs-lookup"><span data-stu-id="48558-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="48558-118">Вызов удаленных методов службы</span><span class="sxs-lookup"><span data-stu-id="48558-118">Call remote service methods</span></span>
<span data-ttu-id="48558-119">Вызов методов службы с помощью удаленного взаимодействия стека hello делается с помощью toohello локальный прокси-службы через hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` класса.</span><span class="sxs-lookup"><span data-stu-id="48558-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="48558-120">Hello `ServiceProxyBase` метод создает локальный прокси-сервер, используя же интерфейс, hello службы реализует hello.</span><span class="sxs-lookup"><span data-stu-id="48558-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="48558-121">С прокси-сервера можно просто вызвать методы интерфейса hello удаленно.</span><span class="sxs-lookup"><span data-stu-id="48558-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="48558-122">Hello удаленного взаимодействия framework распространяет исключения на клиенте toohello hello службы.</span><span class="sxs-lookup"><span data-stu-id="48558-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="48558-123">Поэтому обработка исключений логику на приветствия клиента с помощью `ServiceProxyBase` может напрямую обрабатывать исключения, которые hello служба вызывает исключение.</span><span class="sxs-lookup"><span data-stu-id="48558-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="48558-124">Время существования ServiceProxy</span><span class="sxs-lookup"><span data-stu-id="48558-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="48558-125">Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно.</span><span class="sxs-lookup"><span data-stu-id="48558-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="48558-126">Прокси-сервер службы можно использовать повторно, если он нужен пользователю.</span><span class="sxs-lookup"><span data-stu-id="48558-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="48558-127">Пользователь может повторно использовать hello один прокси-сервер при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="48558-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="48558-128">Каждый ServiceProxy содержит сообщения toosend клиентом обмена данными по сети hello.</span><span class="sxs-lookup"><span data-stu-id="48558-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="48558-129">При вызове API, у нас есть внутренняя проверка toosee Если связи клиента является допустимым.</span><span class="sxs-lookup"><span data-stu-id="48558-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="48558-130">На основании этого результата, создаются заново hello связи клиента.</span><span class="sxs-lookup"><span data-stu-id="48558-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="48558-131">Поэтому пользователь не обязательно serviceproxy toorecreate при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="48558-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="48558-132">Время существования ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="48558-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="48558-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="48558-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="48558-134">Если вы используете API `ServiceProxyBase.create` для создания прокси-сервера, то платформа создает `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="48558-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="48558-135">Это полезно toocreate один вручную при необходимости toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) свойства.</span><span class="sxs-lookup"><span data-stu-id="48558-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="48558-136">Создание фабрики — ресурсоемкая операция.</span><span class="sxs-lookup"><span data-stu-id="48558-136">Factory is an expensive operation.</span></span> <span data-ttu-id="48558-137">`FabricServiceProxyFactory` хранит кэш клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="48558-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="48558-138">Лучший способ — toocache `FabricServiceProxyFactory` то же время.</span><span class="sxs-lookup"><span data-stu-id="48558-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="48558-139">Обработка исключений удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="48558-139">Remoting Exception Handling</span></span>
<span data-ttu-id="48558-140">Все hello удаленного исключение, созданное API службы, как RuntimeException или FabricException отправляются назад toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="48558-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="48558-141">ServiceProxy обрабатывать все исключения отработки отказа для раздела службы hello она создана для.</span><span class="sxs-lookup"><span data-stu-id="48558-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="48558-142">Повторно разрешает hello конечных точек, если имеется вызов hello Exceptions(Non-Transient Exceptions) отработки отказа и повторные попытки с hello правильную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="48558-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="48558-143">Число повторных попыток для исключения отработки отказа не ограничено.</span><span class="sxs-lookup"><span data-stu-id="48558-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="48558-144">В случае TransientExceptions только повторяет вызов hello.</span><span class="sxs-lookup"><span data-stu-id="48558-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="48558-145">Параметры повтора по умолчанию определяются [OperationRetrySettings]</span><span class="sxs-lookup"><span data-stu-id="48558-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="48558-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Пользователь может настроить эти значения, передав конструктору tooServiceProxyFactory OperationRetrySettings объекта.</span><span class="sxs-lookup"><span data-stu-id="48558-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48558-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48558-147">Next steps</span></span>
* [<span data-ttu-id="48558-148">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="48558-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
