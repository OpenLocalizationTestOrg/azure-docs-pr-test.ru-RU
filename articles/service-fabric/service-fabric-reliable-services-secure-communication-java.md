---
title: "aaaHelp безопасную связь для службы в Azure Service Fabric | Документы Microsoft"
description: "Обзор как toohelp безопасности соединения для надежных служб, выполняющихся в кластере Azure Service Fabric."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="29d0c-103">Защита взаимодействия служб в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29d0c-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29d0c-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="29d0c-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="29d0c-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="29d0c-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="29d0c-106">Защита службы при использовании удаленного взаимодействия служб</span><span class="sxs-lookup"><span data-stu-id="29d0c-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="29d0c-107">Мы будем использовать существующий [пример](service-fabric-reliable-services-communication-remoting-java.md) объясняет, как tooset копирование удаленного взаимодействия для надежных служб.</span><span class="sxs-lookup"><span data-stu-id="29d0c-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="29d0c-108">toohelp защиты службы при использовании службы удаленного доступа, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="29d0c-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="29d0c-109">Создайте интерфейс, `HelloWorldStateless`, определяющий hello методы, которые будут доступны для удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="29d0c-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="29d0c-110">Служба будет использовать `FabricTransportServiceRemotingListener`, которое объявлено в hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` пакета.</span><span class="sxs-lookup"><span data-stu-id="29d0c-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="29d0c-111">Это реализация `CommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="29d0c-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="29d0c-112">Добавьте параметры прослушивателя и учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="29d0c-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="29d0c-113">Убедитесь, что hello сертификат, который toouse toohelp безопасной связи службы установлен на всех узлах кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="29d0c-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="29d0c-114">Существует два способа указания параметров прослушивателя и учетных данных безопасности:</span><span class="sxs-lookup"><span data-stu-id="29d0c-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="29d0c-115">Предоставьте их с помощью [пакета конфигурации](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="29d0c-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="29d0c-116">Добавить `TransportSettings` раздел в файле settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="29d0c-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="29d0c-117">В этом случае hello `createServiceInstanceListeners` метода будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29d0c-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="29d0c-118">При добавлении `TransportSettings` раздела в файле settings.xml hello без какого-либо префикса `FabricTransportListenerSettings` будет загружать все параметры hello из этого раздела по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="29d0c-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="29d0c-119">В этом случае hello `CreateServiceInstanceListeners` метода будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29d0c-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="29d0c-120">При вызове методов в службе, защищенной с помощью стека hello удаленного взаимодействия, вместо использования hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate класс прокси-службы, используйте `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="29d0c-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="29d0c-121">Если код клиента hello выполняется как часть службы, можно загрузить `FabricTransportSettings` из файла settings.xml hello.</span><span class="sxs-lookup"><span data-stu-id="29d0c-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="29d0c-122">Создайте раздел TransportSettings, подобный код службы toohello, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="29d0c-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="29d0c-123">Внесите следующие изменения toohello клиентского кода hello:</span><span class="sxs-lookup"><span data-stu-id="29d0c-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
