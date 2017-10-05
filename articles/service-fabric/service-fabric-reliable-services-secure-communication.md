---
title: "Защита взаимодействия служб в Azure Service Fabric | Документация Майкрософт"
description: "Общие сведения о способах защиты взаимодействия служб Reliable Services, выполняющихся в кластере Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="94aae-103">Защита взаимодействия служб в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="94aae-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94aae-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="94aae-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="94aae-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="94aae-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="94aae-106">Безопасность — один из самых важных аспектов взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="94aae-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="94aae-107">Платформа приложений Reliable Services предоставляет несколько готовых стеков взаимодействия и средств, которыми можно воспользоваться для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="94aae-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="94aae-108">В этой статье рассматриваются способы повышения безопасности при использовании удаленного взаимодействия служб и стека взаимодействия Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="94aae-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="94aae-109">Защита службы при использовании удаленного взаимодействия служб</span><span class="sxs-lookup"><span data-stu-id="94aae-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="94aae-110">Мы используем существующий [пример](service-fabric-reliable-services-communication-remoting.md), в котором описывается настройка удаленного взаимодействия для Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="94aae-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="94aae-111">Для защиты службы при использовании удаленного взаимодействия служб выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="94aae-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="94aae-112">Создайте интерфейс `IHelloWorldStateful`, определяющий методы, которые будут доступны для удаленного вызова процедур в службе.</span><span class="sxs-lookup"><span data-stu-id="94aae-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="94aae-113">Служба также будет использовать прослушиватель `FabricTransportServiceRemotingListener`, который объявляется в пространстве имен `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="94aae-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="94aae-114">Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="94aae-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="94aae-115">Добавьте параметры прослушивателя и учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="94aae-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="94aae-116">Убедитесь, что сертификат, который вы хотите использовать для защиты взаимодействия со службой, установлен на всех узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="94aae-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="94aae-117">Существует два способа указания параметров прослушивателя и учетных данных безопасности:</span><span class="sxs-lookup"><span data-stu-id="94aae-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="94aae-118">Предоставьте их непосредственно в коде службы:</span><span class="sxs-lookup"><span data-stu-id="94aae-118">Provide them directly in the service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="94aae-119">Предоставьте их с помощью [пакета конфигурации](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="94aae-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="94aae-120">Добавьте раздел `TransportSettings` в файл settings.xml.</span><span class="sxs-lookup"><span data-stu-id="94aae-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="94aae-121">В этом случае метод `CreateServiceReplicaListeners` будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94aae-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="94aae-122">При добавлении раздела `TransportSettings` в файл settings.xml `FabricTransportRemotingListenerSettings ` по умолчанию загрузит все параметры из этого раздела.</span><span class="sxs-lookup"><span data-stu-id="94aae-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="94aae-123">В этом случае метод `CreateServiceReplicaListeners` будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94aae-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="94aae-124">При вызове методов для защищенной службы с помощью стека удаленного взаимодействия вместо использования класса `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` для создания прокси-службы используйте `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="94aae-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="94aae-125">Передайте параметр `FabricTransportRemotingSettings`, который содержит объект `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="94aae-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="94aae-126">Если клиентский код выполняется как часть службы, можно загрузить `FabricTransportRemotingSettings` из файла settings.xml.</span><span class="sxs-lookup"><span data-stu-id="94aae-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="94aae-127">Создайте раздел HelloWorldClientTransportSettings по аналогии с кодом службы, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="94aae-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="94aae-128">Внесите следующие изменения в клиентский код:</span><span class="sxs-lookup"><span data-stu-id="94aae-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="94aae-129">Если клиент не выполняется как часть службы, можно создать файл client_name.settings.xml в том же каталоге, в котором находится файл client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="94aae-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="94aae-130">Затем создайте раздел TransportSettings в этом файле.</span><span class="sxs-lookup"><span data-stu-id="94aae-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="94aae-131">Как и для службы, если в файл клиента settings.xml/client_name.settings.xml добавить раздел `TransportSettings`, то `FabricTransportRemotingSettings` по умолчанию загрузит все параметры из этого раздела.</span><span class="sxs-lookup"><span data-stu-id="94aae-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="94aae-132">В этом случае приведенный выше код еще более упрощается.</span><span class="sxs-lookup"><span data-stu-id="94aae-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="94aae-133">Защита службы при использовании стека взаимодействия на основе WCF</span><span class="sxs-lookup"><span data-stu-id="94aae-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="94aae-134">Мы используем существующий [пример](service-fabric-reliable-services-communication-wcf.md), в котором описывается настройка стека связи на основе WCF для Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="94aae-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="94aae-135">Для защиты службы при использовании стека взаимодействия на основе WCF выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="94aae-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="94aae-136">Для службы необходимо обеспечить защиту создаваемого прослушивателя взаимодействия WCF (`WcfCommunicationListener`).</span><span class="sxs-lookup"><span data-stu-id="94aae-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="94aae-137">Чтобы сделать это, измените метод `CreateServiceReplicaListeners` .</span><span class="sxs-lookup"><span data-stu-id="94aae-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in the ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="94aae-138">В клиенте класс `WcfCommunicationClient` , созданный в предыдущем [примере](service-fabric-reliable-services-communication-wcf.md) , остается неизменным.</span><span class="sxs-lookup"><span data-stu-id="94aae-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="94aae-139">Однако необходимо переопределить метод `CreateClientAsync` фабрики `WcfCommunicationClientFactory`.</span><span class="sxs-lookup"><span data-stu-id="94aae-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="94aae-140">Используйте `SecureWcfCommunicationClientFactory`, чтобы создать клиент взаимодействия WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="94aae-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="94aae-141">Воспользуйтесь клиентом для вызова методов службы.</span><span class="sxs-lookup"><span data-stu-id="94aae-141">Use the client to invoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="94aae-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94aae-142">Next steps</span></span>
* [<span data-ttu-id="94aae-143">Веб-API с OWIN в модели Reliable Services</span><span class="sxs-lookup"><span data-stu-id="94aae-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
