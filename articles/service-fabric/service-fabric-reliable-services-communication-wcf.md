---
title: "стек связи для служб WCF aaaReliable | Документы Microsoft"
description: "встроенный стек связи WCF Hello в Service Fabric предоставляет службы клиента WCF для надежного обмена."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="49ee6-103">Коммуникационный стек WCF для надежных служб</span><span class="sxs-lookup"><span data-stu-id="49ee6-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="49ee6-104">Надежные службы Hello платформа дает авторам toochoose hello связи стека служб, они должны toouse для своей службы.</span><span class="sxs-lookup"><span data-stu-id="49ee6-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="49ee6-105">Они могут подключить hello стек связи по своему выбору через hello **ICommunicationListener** возвращенные hello [CreateServiceReplicaListeners или CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) методы.</span><span class="sxs-lookup"><span data-stu-id="49ee6-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="49ee6-106">Hello framework предоставляет реализацию hello стек связи, основанного на приветствия Windows Communication Foundation (WCF) для службы авторов, toouse связи на основе WCF.</span><span class="sxs-lookup"><span data-stu-id="49ee6-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="49ee6-107">Прослушиватель связи WCF</span><span class="sxs-lookup"><span data-stu-id="49ee6-107">WCF Communication Listener</span></span>
<span data-ttu-id="49ee6-108">Hello зависящие от WCF реализация **ICommunicationListener** обеспечивается hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** класса.</span><span class="sxs-lookup"><span data-stu-id="49ee6-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="49ee6-109">Допустим, имеется контракт службы типа `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="49ee6-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="49ee6-110">Можно создать прослушиватель связи WCF в следующие способом hello службы hello.</span><span class="sxs-lookup"><span data-stu-id="49ee6-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="49ee6-111">Написание клиентов для стека связи hello WCF</span><span class="sxs-lookup"><span data-stu-id="49ee6-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="49ee6-112">Для записи клиентов, toocommunicate со службами с помощью WCF, hello framework предоставляет **WcfClientCommunicationFactory**, который является реализацией hello WCF конкретного метода [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="49ee6-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="49ee6-113">канал связи WCF Hello может осуществляться из hello **WcfCommunicationClient** созданные hello **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="49ee6-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="49ee6-114">Клиентский код может использовать hello **WcfCommunicationClientFactory** вместе с hello **WcfCommunicationClient** , реализующий **ServicePartitionClient** toodetermine Здравствуйте, конечная точка службы и взаимодействовать со службой hello.</span><span class="sxs-lookup"><span data-stu-id="49ee6-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="49ee6-115">по умолчанию Hello ServicePartitionResolver предполагается, что этот клиент hello выполняется в одном кластере hello службы.</span><span class="sxs-lookup"><span data-stu-id="49ee6-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="49ee6-116">Если это не hello случае создайте объект ServicePartitionResolver и передайте конечные точки подключения кластера hello.</span><span class="sxs-lookup"><span data-stu-id="49ee6-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="49ee6-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49ee6-117">Next steps</span></span>
* [<span data-ttu-id="49ee6-118">Удаленный вызов процедур с использованием удаленного взаимодействия Reliable Services</span><span class="sxs-lookup"><span data-stu-id="49ee6-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="49ee6-119">Веб-интерфейс API с OWIN в Reliable Services</span><span class="sxs-lookup"><span data-stu-id="49ee6-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="49ee6-120">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="49ee6-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

