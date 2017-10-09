---
title: "aaaConnect и взаимодействия со службами в Azure Service Fabric | Документы Microsoft"
description: "Узнайте, как tooresolve, подключения и взаимодействия со службами в Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Подключение к службам в Service Fabric и взаимодействие с ними
Служба Service Fabric, запущенная в кластере Service Fabric, обычно распределена между несколькими виртуальными машинами. Его можно перемещать из tooanother в одном месте, либо владелец службы hello, или автоматически управляются Service Fabric. Службы не статически связанные tooa конкретного компьютера или адрес.

Приложение Service Fabric состоит из множества разных служб, каждая из которых выполняет специализированную задачу. Эти службы могут взаимодействовать с друг с другом tooform функцию завершения, например подготовки к просмотру различных частей веб-приложения. Существуют также клиентские приложения, которые подключаются tooand взаимодействия со службами. В этом документе рассматриваются как tooset скорость связи с, а также между службами в Service Fabric.

В этом видеоролике от Академии Microsoft Virtual Academy также показано взаимодействие служб: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Используйте любой удобный протокол
Service Fabric помогает управлять жизненным циклом hello служб, но его не следует принимать решение о возможностях служб. Это относится и к обмену данными. При открытии службы с Service Fabric, то есть tooset возможности службы доступ к конечной точке для входящих запросов, с помощью любой стек протокола или связи требуется. Служба будет прослушивать обычный адрес в формате **IP:порт** с использованием любой схемы адресации, например URI. Несколько экземпляров службы или реплики могут совместно использовать хост-процесса, в этом случае они будут требуются порты различных toouse или использовать механизм совместное использование порта, например драйвер ядра http.sys hello в Windows. В любом случае все экземпляры или реплики службы в хост-процессе должны быть уникально адресуемыми.

![Конечные точки службы][1]

## <a name="service-discovery-and-resolution"></a>Поиск и разрешение служб
В распределенной системе службы могут перемещаться из одного компьютера tooanother со временем. Это может происходить по разным причинам, например при балансировке, обновлении, отработке отказа или масштабировании ресурсов. Это означает, что изменить адреса конечных точек службы, как служба hello перемещает toonodes различные IP-адреса и может открыть другие порты, если служба hello использует динамически выбранного порта.

![Распределение служб][7]

Service Fabric обеспечивает обнаружение и разрешение, обращение к службе hello службы имен. Hello именования служба поддерживает таблицу, которая сопоставляет именованных экземпляров службы toohello адресов конечных точек, которые они выполняют прослушивание. Все именованные экземпляры службы в Service Fabric имеют уникальные универсальные коды ресурса (URI) в качестве имен, например `"fabric:/MyApplication/MyService"`. Имя Hello hello службы не изменяется за время жизни hello hello службы, это только hello адресов конечных точек, можно изменить при перемещении службы. Это аналог toowebsites, которые имеют постоянное URL-адреса, но где hello IP-адрес может изменить. И аналогичные tooDNS на веб-hello, который разрешает адреса tooIP URL-адреса веб-сайтов, Service Fabric регистратора, который сопоставляет адрес конечной точки службы имен tootheir.

![Конечные точки службы][2]

Разрешение и подключение tooservices включает следующие шаги в цикле hello:

* **Разрешить**: hello Get конечной точки, которая опубликована службы из hello службы имен.
* **Подключение**: подключиться через любое протокола использует в этой конечной точке службы toohello.
* **Повторите**: попытка соединения может завершиться ошибкой по какой-либо причинам, например, если служба hello была перемещена, поскольку hello последнее время адрес конечной точки для hello был разрешен. В этом случае hello предшествующий разрешения и подключение действия требуется повторная toobe, и этот цикл повторяется до успешного завершения подключения hello.

## <a name="connecting-tooother-services"></a>Соединение tooother служб
Службы, подключающиеся tooeach других внутри кластера обычно обеспечивается прямой доступ к hello конечных точек других служб, поскольку hello узлы кластера находятся в hello одной локальной сети. toomake проще tooconnect между службами, Service Fabric предоставляет дополнительные службы, использующие hello службы имен. служба DNS и служба обратного прокси-сервера.


### <a name="dns-service"></a>Служба DNS
Поскольку многие службы, особенно контейнерного службы может иметь имя существующей URL-адрес, которой может tooresolve их, используя hello стандартный протокол DNS (а не протокол службы имен hello) очень удобна, особенно в приложении «точности прогнозов и сдвиг» сценарии. Это именно какие службы DNS hello. Он включает вы toomap DNS имена tooa имя службы и таким образом разрешить IP-адреса конечной точки. 

Как показано в hello следующей схеме hello запуска службы DNS, в кластер Service Fabric hello, сопоставляет DNS-имена tooservice имена, которые затем разрешаются с hello службы имен tooreturn hello конечной точки адреса tooconnect для. Hello DNS-имя для службы hello предоставляется во время создания hello. 

![Конечные точки службы][9]

Дополнительные сведения о статье toouse hello служба DNS [служба DNS в Azure Service Fabric](service-fabric-dnsservice.md) статьи.

### <a name="reverse-proxy-service"></a>Служба обратного прокси-сервера
Hello обратного прокси-сервера адреса службы в кластере hello, который предоставляет конечные точки HTTP, включая HTTPS. Hello обратный прокси-сервер значительно упрощает вызов других служб и их методов с наличием определенный формат URI и дескрипторы устранить hello, подключения, Здравствуйте, повторите шаги, необходимые для одной службы toocommunicate с другой с помощью службы именования. Другими словами он скрывает hello службы именования от вас при вызове других служб, делая это просто вызов URL-адрес.

![Конечные точки службы][10]

Дополнительные сведения о как toouse hello обратного прокси-службы см. в разделе [обратный прокси-сервер в Azure Service Fabric](service-fabric-reverseproxy.md) статьи.

## <a name="connections-from-external-clients"></a>Подключения от внешних клиентов
Службы, подключающиеся tooeach других внутри кластера обычно обеспечивается прямой доступ к hello конечных точек других служб, поскольку hello узлы кластера находятся в hello одной локальной сети. Однако в некоторых средах балансировщик нагрузки, который направляет приходящий извне трафик через ограниченный набор портов, может располагаться за кластером. В таких случаях службы можно по-прежнему взаимодействовать друг с другом и разрешить адресов с помощью hello службы имен, но дополнительные действия должны быть tooservices tooconnect сделанной tooallow внешних клиентов.

## <a name="service-fabric-in-azure"></a>Service Fabric в Azure
Балансировщик нагрузки Azure расположен за кластером Service Fabric в Azure. Все внешнего трафика toohello кластер должен пройти через hello балансировки нагрузки. Hello балансировки нагрузки будет автоматически пересылать трафик входящего трафика на данный порт tooa случайных *узел* с Привет открыть тот же порт. Hello подсистемы балансировки нагрузки Azure только знает о портах, открытых на hello *узлы*, не знает об открытых портов каждым участником *службы*.

![Топология балансировщика нагрузки и Service Fabric в Azure][3]

Например, в порядке tooaccept внешнего трафика через порт **80**, должен быть настроен hello, следующие действия:

1. Создайте службу, прослушивающую порт 80. Настройте порт 80 в файле ServiceManifest.xml службы hello и открыть прослушиватель в службе hello, например, резидентных веб-сервера.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Создание кластера Service Fabric в Azure и указать порт **80** как порт настраиваемую конечную точку для типа узла hello, где будет размещаться служба hello. При наличии более чем один тип узла, можно настроить *ограничения на размещение* на tooensure hello службы, она выполняется только для узлов типа hello, имеющий открыть порт hello пользовательской конечной точки.

    ![Открытие порта для типа узла][4]
3. После создания кластера hello настройте hello подсистемы балансировки нагрузки Azure в кластер hello группы ресурсов tooforward трафик через порт 80. При создании кластера с помощью hello портал Azure, это настройки автоматически для каждого порта пользовательской конечной точки, который был настроен.

    ![Перенаправление трафика в hello подсистемы балансировки нагрузки Azure][5]
4. Здравствуйте Подсистема балансировки нагрузки Azure использует ли toodetermine проверки или не toosend трафика tooa конкретный узел. Hello проверки проверки конечной точки на каждый узел toodetermine, отвечает ли узел hello периодически. При сбое проверки hello tooreceive ответ после определенного числа раз балансировки нагрузки hello перестает отправлять трафик toothat узла. При создании кластера с помощью портала Azure hello, зонда автоматически настраивается для каждого порта пользовательской конечной точки, который был настроен.

    ![Перенаправление трафика в hello подсистемы балансировки нагрузки Azure][8]

Это важные tooremember, hello подсистемы балансировки нагрузки Azure и проверки hello только о hello *узлы*, не hello *служб* на узлах hello. Hello подсистемы балансировки нагрузки Azure всегда будут отправлять toonodes трафика, ответить toohello проверки, поэтому будьте внимательны tooensure службы доступны в hello узлы, которые являются может toorespond toohello проверки.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services. Встроенные варианты API для обмена данными
Hello framework надежного обмена поставляется с несколькими параметрами готовые связи. Hello принятия решений о том, какие один наилучшим образом подходит для вас зависит от выбора hello hello программирования модели, платформа взаимодействия hello и hello, служб, написанные на языке программирования.

* **Нет определенного протокола:** Если не нужно, чтобы тот или иной Выбор communication Framework, но требуется tooget что-нибудь и быстро, то hello идеальным вариантом является [службы удаленного взаимодействия](service-fabric-reliable-services-communication-remoting.md), что позволяет строго типизированные удаленные вызовы процедур для надежных служб и службы Reliable Actor. Это простой hello и tooget самый быстрый способ работы с связь со службой. Удаленное взаимодействие между службами берет на себя разрешение адреса службы, процедуры подключения, повторных попыток и обработки ошибок. Эта возможность доступна для приложений на C# и Java.
* **HTTP**: протокол HTTP — это стандартный вариант для обмена данными между системами на любых языках. Платформа Service Fabric поддерживает любые средства для HTTP и HTTP-серверы, доступные для множества языков. Службы могут использовать любой из существующих стеков HTTP, в том числе [веб-API ASP.NET](service-fabric-reliable-services-communication-webapi.md) для приложений на C#. Клиенты, написанные на языке C# могут использовать hello `ICommunicationClient` и `ServicePartitionClient` классы, в то время как для Java, используйте hello `CommunicationClient` и `FabricServicePartitionClient` классы, [разрешения для службы, HTTP-соединений и циклов повтора](service-fabric-reliable-services-communication.md).
* **WCF**: Если имеется существующий код, использующий WCF в качестве вашей платформы связи, то можно использовать hello `WcfCommunicationListener` hello на стороне сервера и `WcfCommunicationClient` и `ServicePartitionClient` классы для клиента hello. Но это доступно только для приложений на C# в кластерах на платформе Windows. Дополнительные сведения см. статью [реализация hello стек связи на основе WCF](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Использование пользовательских протоколов и других платформ для обмена данными
Ваши службы могут использовать для обмена данными любой протокол и любую платформу, будь то пользовательский двоичный протокол, работающий через сокеты TCP, или события потоковой передачи с использованием [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) или [Центра Интернета вещей Azure](https://azure.microsoft.com/services/iot-hub/). Предоставляет Service Fabric связи API, которые можно подключить к стек связи, пока все hello работать toodiscover и связывать абстрагируется от вас. См. в статье о hello [модель взаимодействия надежной службы](service-fabric-reliable-services-communication.md) для получения дополнительных сведений.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о концепции hello и API-интерфейса в hello [модель взаимодействия надежного обмена](service-fabric-reliable-services-communication.md), затем быстро приступить к работе с [службы удаленного взаимодействия](service-fabric-reliable-services-communication-remoting.md) или подробные toolearn как toowrite связи прослушивателя с помощью [веб-API с резидентной OWIN](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
