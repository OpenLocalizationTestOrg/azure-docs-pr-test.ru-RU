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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Защита взаимодействия служб в Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java в Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

Безопасность — один из самых важных аспектов взаимодействия. Платформа приложений Reliable Services предоставляет несколько готовых стеков взаимодействия и средств, которыми можно воспользоваться для повышения безопасности. В этой статье рассматриваются способы повышения безопасности при использовании удаленного взаимодействия служб и стека взаимодействия Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Защита службы при использовании удаленного взаимодействия служб
Мы используем существующий [пример](service-fabric-reliable-services-communication-remoting.md), в котором описывается настройка удаленного взаимодействия для Reliable Services. Для защиты службы при использовании удаленного взаимодействия служб выполните следующие действия:

1. Создайте интерфейс `IHelloWorldStateful`, определяющий методы, которые будут доступны для удаленного вызова процедур в службе. Служба также будет использовать прослушиватель `FabricTransportServiceRemotingListener`, который объявляется в пространстве имен `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime`. Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия.

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
2. Добавьте параметры прослушивателя и учетные данные безопасности.

    Убедитесь, что сертификат, который вы хотите использовать для защиты взаимодействия со службой, установлен на всех узлах в кластере. Существует два способа указания параметров прослушивателя и учетных данных безопасности:

   1. Предоставьте их непосредственно в коде службы:

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
   2. Предоставьте их с помощью [пакета конфигурации](service-fabric-application-model.md):

       Добавьте раздел `TransportSettings` в файл settings.xml.

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

       В этом случае метод `CreateServiceReplicaListeners` будет выглядеть следующим образом:

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

        При добавлении раздела `TransportSettings` в файл settings.xml `FabricTransportRemotingListenerSettings ` по умолчанию загрузит все параметры из этого раздела.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        В этом случае метод `CreateServiceReplicaListeners` будет выглядеть следующим образом:

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
3. При вызове методов для защищенной службы с помощью стека удаленного взаимодействия вместо использования класса `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` для создания прокси-службы используйте `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Передайте параметр `FabricTransportRemotingSettings`, который содержит объект `SecurityCredentials`.

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

    Если клиентский код выполняется как часть службы, можно загрузить `FabricTransportRemotingSettings` из файла settings.xml. Создайте раздел HelloWorldClientTransportSettings по аналогии с кодом службы, как показано выше. Внесите следующие изменения в клиентский код:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Если клиент не выполняется как часть службы, можно создать файл client_name.settings.xml в том же каталоге, в котором находится файл client_name.exe. Затем создайте раздел TransportSettings в этом файле.

    Как и для службы, если в файл клиента settings.xml/client_name.settings.xml добавить раздел `TransportSettings`, то `FabricTransportRemotingSettings` по умолчанию загрузит все параметры из этого раздела.

    В этом случае приведенный выше код еще более упрощается.  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Защита службы при использовании стека взаимодействия на основе WCF
Мы используем существующий [пример](service-fabric-reliable-services-communication-wcf.md), в котором описывается настройка стека связи на основе WCF для Reliable Services. Для защиты службы при использовании стека взаимодействия на основе WCF выполните следующие действия:

1. Для службы необходимо обеспечить защиту создаваемого прослушивателя взаимодействия WCF (`WcfCommunicationListener`). Чтобы сделать это, измените метод `CreateServiceReplicaListeners` .

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
2. В клиенте класс `WcfCommunicationClient` , созданный в предыдущем [примере](service-fabric-reliable-services-communication-wcf.md) , остается неизменным. Однако необходимо переопределить метод `CreateClientAsync` фабрики `WcfCommunicationClientFactory`.

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

    Используйте `SecureWcfCommunicationClientFactory`, чтобы создать клиент взаимодействия WCF (`WcfCommunicationClient`). Воспользуйтесь клиентом для вызова методов службы.

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

## <a name="next-steps"></a>Дальнейшие действия
* [Веб-API с OWIN в модели Reliable Services](service-fabric-reliable-services-communication-webapi.md)
