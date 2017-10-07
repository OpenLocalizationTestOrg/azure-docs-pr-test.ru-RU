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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Защита взаимодействия служб в Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java в Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Защита службы при использовании удаленного взаимодействия служб
Мы будем использовать существующий [пример](service-fabric-reliable-services-communication-remoting-java.md) объясняет, как tooset копирование удаленного взаимодействия для надежных служб. toohelp защиты службы при использовании службы удаленного доступа, выполните следующие действия:

1. Создайте интерфейс, `HelloWorldStateless`, определяющий hello методы, которые будут доступны для удаленного вызова процедур для службы. Служба будет использовать `FabricTransportServiceRemotingListener`, которое объявлено в hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` пакета. Это реализация `CommunicationListener` , которая предоставляет возможности удаленного взаимодействия.

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
2. Добавьте параметры прослушивателя и учетные данные безопасности.

    Убедитесь, что hello сертификат, который toouse toohelp безопасной связи службы установлен на всех узлах кластера hello hello. Существует два способа указания параметров прослушивателя и учетных данных безопасности:

   1. Предоставьте их с помощью [пакета конфигурации](service-fabric-application-model.md):

       Добавить `TransportSettings` раздел в файле settings.xml hello.

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

       В этом случае hello `createServiceInstanceListeners` метода будет выглядеть следующим образом:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        При добавлении `TransportSettings` раздела в файле settings.xml hello без какого-либо префикса `FabricTransportListenerSettings` будет загружать все параметры hello из этого раздела по умолчанию.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        В этом случае hello `CreateServiceInstanceListeners` метода будет выглядеть следующим образом:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. При вызове методов в службе, защищенной с помощью стека hello удаленного взаимодействия, вместо использования hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` toocreate класс прокси-службы, используйте `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Если код клиента hello выполняется как часть службы, можно загрузить `FabricTransportSettings` из файла settings.xml hello. Создайте раздел TransportSettings, подобный код службы toohello, как показано выше. Внесите следующие изменения toohello клиентского кода hello:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
