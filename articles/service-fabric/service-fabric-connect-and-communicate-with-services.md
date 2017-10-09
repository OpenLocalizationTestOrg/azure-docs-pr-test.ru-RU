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
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="f705a-103">Подключение к службам в Service Fabric и взаимодействие с ними</span><span class="sxs-lookup"><span data-stu-id="f705a-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="f705a-104">Служба Service Fabric, запущенная в кластере Service Fabric, обычно распределена между несколькими виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="f705a-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="f705a-105">Его можно перемещать из tooanother в одном месте, либо владелец службы hello, или автоматически управляются Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f705a-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="f705a-106">Службы не статически связанные tooa конкретного компьютера или адрес.</span><span class="sxs-lookup"><span data-stu-id="f705a-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="f705a-107">Приложение Service Fabric состоит из множества разных служб, каждая из которых выполняет специализированную задачу.</span><span class="sxs-lookup"><span data-stu-id="f705a-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="f705a-108">Эти службы могут взаимодействовать с друг с другом tooform функцию завершения, например подготовки к просмотру различных частей веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f705a-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="f705a-109">Существуют также клиентские приложения, которые подключаются tooand взаимодействия со службами.</span><span class="sxs-lookup"><span data-stu-id="f705a-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="f705a-110">В этом документе рассматриваются как tooset скорость связи с, а также между службами в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f705a-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="f705a-111">В этом видеоролике от Академии Microsoft Virtual Academy также показано взаимодействие служб: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="f705a-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="f705a-112">Используйте любой удобный протокол</span><span class="sxs-lookup"><span data-stu-id="f705a-112">Bring your own protocol</span></span>
<span data-ttu-id="f705a-113">Service Fabric помогает управлять жизненным циклом hello служб, но его не следует принимать решение о возможностях служб.</span><span class="sxs-lookup"><span data-stu-id="f705a-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="f705a-114">Это относится и к обмену данными.</span><span class="sxs-lookup"><span data-stu-id="f705a-114">This includes communication.</span></span> <span data-ttu-id="f705a-115">При открытии службы с Service Fabric, то есть tooset возможности службы доступ к конечной точке для входящих запросов, с помощью любой стек протокола или связи требуется.</span><span class="sxs-lookup"><span data-stu-id="f705a-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="f705a-116">Служба будет прослушивать обычный адрес в формате **IP:порт** с использованием любой схемы адресации, например URI.</span><span class="sxs-lookup"><span data-stu-id="f705a-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="f705a-117">Несколько экземпляров службы или реплики могут совместно использовать хост-процесса, в этом случае они будут требуются порты различных toouse или использовать механизм совместное использование порта, например драйвер ядра http.sys hello в Windows.</span><span class="sxs-lookup"><span data-stu-id="f705a-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="f705a-118">В любом случае все экземпляры или реплики службы в хост-процессе должны быть уникально адресуемыми.</span><span class="sxs-lookup"><span data-stu-id="f705a-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Конечные точки службы][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="f705a-120">Поиск и разрешение служб</span><span class="sxs-lookup"><span data-stu-id="f705a-120">Service discovery and resolution</span></span>
<span data-ttu-id="f705a-121">В распределенной системе службы могут перемещаться из одного компьютера tooanother со временем.</span><span class="sxs-lookup"><span data-stu-id="f705a-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="f705a-122">Это может происходить по разным причинам, например при балансировке, обновлении, отработке отказа или масштабировании ресурсов. Это означает, что изменить адреса конечных точек службы, как служба hello перемещает toonodes различные IP-адреса и может открыть другие порты, если служба hello использует динамически выбранного порта.</span><span class="sxs-lookup"><span data-stu-id="f705a-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Распределение служб][7]

<span data-ttu-id="f705a-124">Service Fabric обеспечивает обнаружение и разрешение, обращение к службе hello службы имен.</span><span class="sxs-lookup"><span data-stu-id="f705a-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="f705a-125">Hello именования служба поддерживает таблицу, которая сопоставляет именованных экземпляров службы toohello адресов конечных точек, которые они выполняют прослушивание.</span><span class="sxs-lookup"><span data-stu-id="f705a-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="f705a-126">Все именованные экземпляры службы в Service Fabric имеют уникальные универсальные коды ресурса (URI) в качестве имен, например `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="f705a-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="f705a-127">Имя Hello hello службы не изменяется за время жизни hello hello службы, это только hello адресов конечных точек, можно изменить при перемещении службы.</span><span class="sxs-lookup"><span data-stu-id="f705a-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="f705a-128">Это аналог toowebsites, которые имеют постоянное URL-адреса, но где hello IP-адрес может изменить.</span><span class="sxs-lookup"><span data-stu-id="f705a-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="f705a-129">И аналогичные tooDNS на веб-hello, который разрешает адреса tooIP URL-адреса веб-сайтов, Service Fabric регистратора, который сопоставляет адрес конечной точки службы имен tootheir.</span><span class="sxs-lookup"><span data-stu-id="f705a-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![Конечные точки службы][2]

<span data-ttu-id="f705a-131">Разрешение и подключение tooservices включает следующие шаги в цикле hello:</span><span class="sxs-lookup"><span data-stu-id="f705a-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="f705a-132">**Разрешить**: hello Get конечной точки, которая опубликована службы из hello службы имен.</span><span class="sxs-lookup"><span data-stu-id="f705a-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="f705a-133">**Подключение**: подключиться через любое протокола использует в этой конечной точке службы toohello.</span><span class="sxs-lookup"><span data-stu-id="f705a-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="f705a-134">**Повторите**: попытка соединения может завершиться ошибкой по какой-либо причинам, например, если служба hello была перемещена, поскольку hello последнее время адрес конечной точки для hello был разрешен.</span><span class="sxs-lookup"><span data-stu-id="f705a-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="f705a-135">В этом случае hello предшествующий разрешения и подключение действия требуется повторная toobe, и этот цикл повторяется до успешного завершения подключения hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="f705a-136">Соединение tooother служб</span><span class="sxs-lookup"><span data-stu-id="f705a-136">Connecting tooother services</span></span>
<span data-ttu-id="f705a-137">Службы, подключающиеся tooeach других внутри кластера обычно обеспечивается прямой доступ к hello конечных точек других служб, поскольку hello узлы кластера находятся в hello одной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="f705a-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="f705a-138">toomake проще tooconnect между службами, Service Fabric предоставляет дополнительные службы, использующие hello службы имен.</span><span class="sxs-lookup"><span data-stu-id="f705a-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="f705a-139">служба DNS и служба обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f705a-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="f705a-140">Служба DNS</span><span class="sxs-lookup"><span data-stu-id="f705a-140">DNS service</span></span>
<span data-ttu-id="f705a-141">Поскольку многие службы, особенно контейнерного службы может иметь имя существующей URL-адрес, которой может tooresolve их, используя hello стандартный протокол DNS (а не протокол службы имен hello) очень удобна, особенно в приложении «точности прогнозов и сдвиг» сценарии.</span><span class="sxs-lookup"><span data-stu-id="f705a-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="f705a-142">Это именно какие службы DNS hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="f705a-143">Он включает вы toomap DNS имена tooa имя службы и таким образом разрешить IP-адреса конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f705a-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="f705a-144">Как показано в hello следующей схеме hello запуска службы DNS, в кластер Service Fabric hello, сопоставляет DNS-имена tooservice имена, которые затем разрешаются с hello службы имен tooreturn hello конечной точки адреса tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="f705a-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="f705a-145">Hello DNS-имя для службы hello предоставляется во время создания hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Конечные точки службы][9]

<span data-ttu-id="f705a-147">Дополнительные сведения о статье toouse hello служба DNS [служба DNS в Azure Service Fabric](service-fabric-dnsservice.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f705a-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="f705a-148">Служба обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="f705a-148">Reverse proxy service</span></span>
<span data-ttu-id="f705a-149">Hello обратного прокси-сервера адреса службы в кластере hello, который предоставляет конечные точки HTTP, включая HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f705a-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="f705a-150">Hello обратный прокси-сервер значительно упрощает вызов других служб и их методов с наличием определенный формат URI и дескрипторы устранить hello, подключения, Здравствуйте, повторите шаги, необходимые для одной службы toocommunicate с другой с помощью службы именования.</span><span class="sxs-lookup"><span data-stu-id="f705a-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="f705a-151">Другими словами он скрывает hello службы именования от вас при вызове других служб, делая это просто вызов URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f705a-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Конечные точки службы][10]

<span data-ttu-id="f705a-153">Дополнительные сведения о как toouse hello обратного прокси-службы см. в разделе [обратный прокси-сервер в Azure Service Fabric](service-fabric-reverseproxy.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f705a-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="f705a-154">Подключения от внешних клиентов</span><span class="sxs-lookup"><span data-stu-id="f705a-154">Connections from external clients</span></span>
<span data-ttu-id="f705a-155">Службы, подключающиеся tooeach других внутри кластера обычно обеспечивается прямой доступ к hello конечных точек других служб, поскольку hello узлы кластера находятся в hello одной локальной сети.</span><span class="sxs-lookup"><span data-stu-id="f705a-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="f705a-156">Однако в некоторых средах балансировщик нагрузки, который направляет приходящий извне трафик через ограниченный набор портов, может располагаться за кластером.</span><span class="sxs-lookup"><span data-stu-id="f705a-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="f705a-157">В таких случаях службы можно по-прежнему взаимодействовать друг с другом и разрешить адресов с помощью hello службы имен, но дополнительные действия должны быть tooservices tooconnect сделанной tooallow внешних клиентов.</span><span class="sxs-lookup"><span data-stu-id="f705a-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="f705a-158">Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="f705a-158">Service Fabric in Azure</span></span>
<span data-ttu-id="f705a-159">Балансировщик нагрузки Azure расположен за кластером Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="f705a-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="f705a-160">Все внешнего трафика toohello кластер должен пройти через hello балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f705a-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="f705a-161">Hello балансировки нагрузки будет автоматически пересылать трафик входящего трафика на данный порт tooa случайных *узел* с Привет открыть тот же порт.</span><span class="sxs-lookup"><span data-stu-id="f705a-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="f705a-162">Hello подсистемы балансировки нагрузки Azure только знает о портах, открытых на hello *узлы*, не знает об открытых портов каждым участником *службы*.</span><span class="sxs-lookup"><span data-stu-id="f705a-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Топология балансировщика нагрузки и Service Fabric в Azure][3]

<span data-ttu-id="f705a-164">Например, в порядке tooaccept внешнего трафика через порт **80**, должен быть настроен hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f705a-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="f705a-165">Создайте службу, прослушивающую порт 80.</span><span class="sxs-lookup"><span data-stu-id="f705a-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="f705a-166">Настройте порт 80 в файле ServiceManifest.xml службы hello и открыть прослушиватель в службе hello, например, резидентных веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="f705a-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="f705a-167">Создание кластера Service Fabric в Azure и указать порт **80** как порт настраиваемую конечную точку для типа узла hello, где будет размещаться служба hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="f705a-168">При наличии более чем один тип узла, можно настроить *ограничения на размещение* на tooensure hello службы, она выполняется только для узлов типа hello, имеющий открыть порт hello пользовательской конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f705a-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Открытие порта для типа узла][4]
3. <span data-ttu-id="f705a-170">После создания кластера hello настройте hello подсистемы балансировки нагрузки Azure в кластер hello группы ресурсов tooforward трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="f705a-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="f705a-171">При создании кластера с помощью hello портал Azure, это настройки автоматически для каждого порта пользовательской конечной точки, который был настроен.</span><span class="sxs-lookup"><span data-stu-id="f705a-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Перенаправление трафика в hello подсистемы балансировки нагрузки Azure][5]
4. <span data-ttu-id="f705a-173">Здравствуйте Подсистема балансировки нагрузки Azure использует ли toodetermine проверки или не toosend трафика tooa конкретный узел.</span><span class="sxs-lookup"><span data-stu-id="f705a-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="f705a-174">Hello проверки проверки конечной точки на каждый узел toodetermine, отвечает ли узел hello периодически.</span><span class="sxs-lookup"><span data-stu-id="f705a-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="f705a-175">При сбое проверки hello tooreceive ответ после определенного числа раз балансировки нагрузки hello перестает отправлять трафик toothat узла.</span><span class="sxs-lookup"><span data-stu-id="f705a-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="f705a-176">При создании кластера с помощью портала Azure hello, зонда автоматически настраивается для каждого порта пользовательской конечной точки, который был настроен.</span><span class="sxs-lookup"><span data-stu-id="f705a-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Перенаправление трафика в hello подсистемы балансировки нагрузки Azure][8]

<span data-ttu-id="f705a-178">Это важные tooremember, hello подсистемы балансировки нагрузки Azure и проверки hello только о hello *узлы*, не hello *служб* на узлах hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="f705a-179">Hello подсистемы балансировки нагрузки Azure всегда будут отправлять toonodes трафика, ответить toohello проверки, поэтому будьте внимательны tooensure службы доступны в hello узлы, которые являются может toorespond toohello проверки.</span><span class="sxs-lookup"><span data-stu-id="f705a-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="f705a-180">Reliable Services. Встроенные варианты API для обмена данными</span><span class="sxs-lookup"><span data-stu-id="f705a-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="f705a-181">Hello framework надежного обмена поставляется с несколькими параметрами готовые связи.</span><span class="sxs-lookup"><span data-stu-id="f705a-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="f705a-182">Hello принятия решений о том, какие один наилучшим образом подходит для вас зависит от выбора hello hello программирования модели, платформа взаимодействия hello и hello, служб, написанные на языке программирования.</span><span class="sxs-lookup"><span data-stu-id="f705a-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="f705a-183">**Нет определенного протокола:** Если не нужно, чтобы тот или иной Выбор communication Framework, но требуется tooget что-нибудь и быстро, то hello идеальным вариантом является [службы удаленного взаимодействия](service-fabric-reliable-services-communication-remoting.md), что позволяет строго типизированные удаленные вызовы процедур для надежных служб и службы Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="f705a-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="f705a-184">Это простой hello и tooget самый быстрый способ работы с связь со службой.</span><span class="sxs-lookup"><span data-stu-id="f705a-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="f705a-185">Удаленное взаимодействие между службами берет на себя разрешение адреса службы, процедуры подключения, повторных попыток и обработки ошибок.</span><span class="sxs-lookup"><span data-stu-id="f705a-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="f705a-186">Эта возможность доступна для приложений на C# и Java.</span><span class="sxs-lookup"><span data-stu-id="f705a-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="f705a-187">**HTTP**: протокол HTTP — это стандартный вариант для обмена данными между системами на любых языках. Платформа Service Fabric поддерживает любые средства для HTTP и HTTP-серверы, доступные для множества языков.</span><span class="sxs-lookup"><span data-stu-id="f705a-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="f705a-188">Службы могут использовать любой из существующих стеков HTTP, в том числе [веб-API ASP.NET](service-fabric-reliable-services-communication-webapi.md) для приложений на C#.</span><span class="sxs-lookup"><span data-stu-id="f705a-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="f705a-189">Клиенты, написанные на языке C# могут использовать hello `ICommunicationClient` и `ServicePartitionClient` классы, в то время как для Java, используйте hello `CommunicationClient` и `FabricServicePartitionClient` классы, [разрешения для службы, HTTP-соединений и циклов повтора](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="f705a-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="f705a-190">**WCF**: Если имеется существующий код, использующий WCF в качестве вашей платформы связи, то можно использовать hello `WcfCommunicationListener` hello на стороне сервера и `WcfCommunicationClient` и `ServicePartitionClient` классы для клиента hello.</span><span class="sxs-lookup"><span data-stu-id="f705a-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="f705a-191">Но это доступно только для приложений на C# в кластерах на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="f705a-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="f705a-192">Дополнительные сведения см. статью [реализация hello стек связи на основе WCF](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="f705a-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="f705a-193">Использование пользовательских протоколов и других платформ для обмена данными</span><span class="sxs-lookup"><span data-stu-id="f705a-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="f705a-194">Ваши службы могут использовать для обмена данными любой протокол и любую платформу, будь то пользовательский двоичный протокол, работающий через сокеты TCP, или события потоковой передачи с использованием [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) или [Центра Интернета вещей Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="f705a-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="f705a-195">Предоставляет Service Fabric связи API, которые можно подключить к стек связи, пока все hello работать toodiscover и связывать абстрагируется от вас.</span><span class="sxs-lookup"><span data-stu-id="f705a-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="f705a-196">См. в статье о hello [модель взаимодействия надежной службы](service-fabric-reliable-services-communication.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="f705a-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f705a-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f705a-197">Next steps</span></span>
<span data-ttu-id="f705a-198">Дополнительные сведения о концепции hello и API-интерфейса в hello [модель взаимодействия надежного обмена](service-fabric-reliable-services-communication.md), затем быстро приступить к работе с [службы удаленного взаимодействия](service-fabric-reliable-services-communication-remoting.md) или подробные toolearn как toowrite связи прослушивателя с помощью [веб-API с резидентной OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="f705a-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
