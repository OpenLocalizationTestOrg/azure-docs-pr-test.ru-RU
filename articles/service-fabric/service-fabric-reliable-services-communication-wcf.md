---
title: "Стек связи WCF Reliable Services | Документация Майкрософт"
description: "Встроенный стек связи WCF в Service Fabric обеспечивает связь со службой клиента WCF для Reliable Services."
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="69b13-103">Коммуникационный стек WCF для надежных служб</span><span class="sxs-lookup"><span data-stu-id="69b13-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="69b13-104">Платформа надежных служб Reliable Services позволяет разработчикам служб решать, какой стек связи следует использовать в службе.</span><span class="sxs-lookup"><span data-stu-id="69b13-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="69b13-105">Любой стек связи можно подключить с помощью интерфейса **ICommunicationListener** , возвращаемого методом [CreateServiceReplicaListeners или CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) .</span><span class="sxs-lookup"><span data-stu-id="69b13-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="69b13-106">Платформа предоставляет реализацию стека связи на основе Windows Communication Foundation (WCF) для разработчиков служб, которым требуется использовать связь на основе WCF.</span><span class="sxs-lookup"><span data-stu-id="69b13-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="69b13-107">Прослушиватель связи WCF</span><span class="sxs-lookup"><span data-stu-id="69b13-107">WCF Communication Listener</span></span>
<span data-ttu-id="69b13-108">Реализация интерфейса **ICommunicationListener**, ориентированная на WCF, обеспечивается классом **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**.</span><span class="sxs-lookup"><span data-stu-id="69b13-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="69b13-109">Допустим, имеется контракт службы типа `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="69b13-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="69b13-110">Мы можем создать прослушиватель связи WCF в службе, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="69b13-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="69b13-111">Написание клиентов для стека связи WCF</span><span class="sxs-lookup"><span data-stu-id="69b13-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="69b13-112">Для написания клиентов для взаимодействия со службами с помощью WCF платформа предоставляет объект **WcfClientCommunicationFactory**, который является ориентированной на WCF реализацией [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="69b13-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="69b13-113">К каналу связи WCF можно обращаться из клиента **WcfCommunicationClient**, созданного объектом **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="69b13-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="69b13-114">Клиентский код может использовать **WcfCommunicationClientFactory** вместе с клиентом **WcfCommunicationClient**, который реализует **ServicePartitionClient**, для определения конечной точки службы и взаимодействия со службой.</span><span class="sxs-lookup"><span data-stu-id="69b13-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="69b13-115">Объект ServicePartitionResolver по умолчанию предполагает, что клиент выполняется в том же кластере, что и служба.</span><span class="sxs-lookup"><span data-stu-id="69b13-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="69b13-116">Если это не так, создайте объект ServicePartitionResolver и передайте конечные точки подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="69b13-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="69b13-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69b13-117">Next steps</span></span>
* [<span data-ttu-id="69b13-118">Удаленный вызов процедур с использованием удаленного взаимодействия Reliable Services</span><span class="sxs-lookup"><span data-stu-id="69b13-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="69b13-119">Веб-интерфейс API с OWIN в Reliable Services</span><span class="sxs-lookup"><span data-stu-id="69b13-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="69b13-120">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="69b13-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

