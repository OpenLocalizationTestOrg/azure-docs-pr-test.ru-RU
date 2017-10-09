---
title: "aaaHelp безопасную связь для службы в Azure Service Fabric | Документы Microsoft"
description: "Обзор как toohelp безопасности соединения для надежных служб, выполняющихся в кластере Azure Service Fabric."
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
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="cbc26-103">Защита взаимодействия служб в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cbc26-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cbc26-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="cbc26-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="cbc26-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="cbc26-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="cbc26-106">Безопасность является одним из самых важных аспектов hello связи.</span><span class="sxs-lookup"><span data-stu-id="cbc26-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="cbc26-107">Платформа приложения Hello надежные службы предоставляет несколько готовых связи стеки и средства, которые можно использовать tooimprove безопасности.</span><span class="sxs-lookup"><span data-stu-id="cbc26-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="cbc26-108">В этой статье рассказывается о tooimprove безопасности при использовании службы удаленного взаимодействия и hello стек связи Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="cbc26-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="cbc26-109">Защита службы при использовании удаленного взаимодействия служб</span><span class="sxs-lookup"><span data-stu-id="cbc26-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="cbc26-110">Мы используем существующего [пример](service-fabric-reliable-services-communication-remoting.md) объясняет, как tooset копирование удаленного взаимодействия для надежного обмена.</span><span class="sxs-lookup"><span data-stu-id="cbc26-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="cbc26-111">toohelp защиты службы при использовании службы удаленного доступа, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cbc26-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="cbc26-112">Создайте интерфейс, `IHelloWorldStateful`, определяющий hello методы, которые будут доступны для удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="cbc26-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="cbc26-113">Служба будет использовать `FabricTransportServiceRemotingListener`, которое объявлено в hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="cbc26-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="cbc26-114">Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="cbc26-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="cbc26-115">Добавьте параметры прослушивателя и учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="cbc26-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="cbc26-116">Убедитесь, что hello сертификат, который toouse toohelp безопасной связи службы установлен на всех узлах кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="cbc26-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="cbc26-117">Существует два способа указания параметров прослушивателя и учетных данных безопасности:</span><span class="sxs-lookup"><span data-stu-id="cbc26-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="cbc26-118">Укажите их непосредственно в код службы hello:</span><span class="sxs-lookup"><span data-stu-id="cbc26-118">Provide them directly in hello service code:</span></span>

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
   2. <span data-ttu-id="cbc26-119">Предоставьте их с помощью [пакета конфигурации](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="cbc26-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="cbc26-120">Добавить `TransportSettings` раздел в файле settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="cbc26-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="cbc26-121">В этом случае hello `CreateServiceReplicaListeners` метода будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cbc26-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="cbc26-122">При добавлении `TransportSettings` раздела в файле settings.xml hello, `FabricTransportRemotingListenerSettings ` будет загружать все параметры hello из этого раздела по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cbc26-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="cbc26-123">В этом случае hello `CreateServiceReplicaListeners` метода будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cbc26-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="cbc26-124">При вызове методов в службе, защищенной с помощью стека hello удаленного взаимодействия, вместо использования hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` toocreate класс прокси-службы, используйте `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="cbc26-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="cbc26-125">Передайте параметр `FabricTransportRemotingSettings`, который содержит объект `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="cbc26-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="cbc26-126">Если код клиента hello выполняется как часть службы, можно загрузить `FabricTransportRemotingSettings` из файла settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="cbc26-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="cbc26-127">Создайте раздел HelloWorldClientTransportSettings, подобный код службы toohello, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="cbc26-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="cbc26-128">Внесите следующие изменения toohello клиентского кода hello:</span><span class="sxs-lookup"><span data-stu-id="cbc26-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="cbc26-129">Если клиент hello не работает как часть службы, можно создать файл client_name.settings.xml в hello же место, где hello client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="cbc26-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="cbc26-130">Затем создайте раздел TransportSettings в этом файле.</span><span class="sxs-lookup"><span data-stu-id="cbc26-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="cbc26-131">Аналогичную службу toohello при добавлении `TransportSettings` раздела settings.xml/client_name.settings.xml клиента `FabricTransportRemotingSettings` загружает все параметры hello из этого раздела по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cbc26-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="cbc26-132">В этом случае hello предыдущих еще больше упростит код:</span><span class="sxs-lookup"><span data-stu-id="cbc26-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="cbc26-133">Защита службы при использовании стека взаимодействия на основе WCF</span><span class="sxs-lookup"><span data-stu-id="cbc26-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="cbc26-134">Мы используем существующего [пример](service-fabric-reliable-services-communication-wcf.md) , объясняется, как tooset вверх связи на основе WCF стека для надежного обмена.</span><span class="sxs-lookup"><span data-stu-id="cbc26-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="cbc26-135">toohelp защиты службы при использовании стека связи на основе WCF, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cbc26-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="cbc26-136">Для службы hello необходимо toohelp безопасного hello WCF связи прослушивателя (`WcfCommunicationListener`), вы создаете.</span><span class="sxs-lookup"><span data-stu-id="cbc26-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="cbc26-137">toodo это, измените hello `CreateServiceReplicaListeners` метод.</span><span class="sxs-lookup"><span data-stu-id="cbc26-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in hello ServiceHost credentials.
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
2. <span data-ttu-id="cbc26-138">В клиенте hello hello `WcfCommunicationClient` класс, который был создан в hello предыдущих [пример](service-fabric-reliable-services-communication-wcf.md) остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="cbc26-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="cbc26-139">Но необходимо toooverride hello `CreateClientAsync` метод `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="cbc26-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
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

    <span data-ttu-id="cbc26-140">Используйте `SecureWcfCommunicationClientFactory` toocreate связи клиента WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="cbc26-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="cbc26-141">Используйте методы службы tooinvoke hello клиента.</span><span class="sxs-lookup"><span data-stu-id="cbc26-141">Use hello client tooinvoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cbc26-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cbc26-142">Next steps</span></span>
* [<span data-ttu-id="cbc26-143">Веб-API с OWIN в модели Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cbc26-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
