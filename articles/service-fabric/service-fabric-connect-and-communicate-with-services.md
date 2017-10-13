---
title: "Взаимодействие со службами в Azure Service Fabric и подключение к ним | Документация Майкрософт"
description: "Узнайте, как разрешать адреса служб на платформе Service Fabric, подключаться к ним и взаимодействовать с ними."
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
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Подключение к службам в Service Fabric и взаимодействие с ними
Служба Service Fabric, запущенная в кластере Service Fabric, обычно распределена между несколькими виртуальными машинами. Владелец службы или платформа Service Fabric могут перемещать ее из одного расположения в другое. Службы не привязаны статически к определенному компьютеру или адресу.

Приложение Service Fabric состоит из множества разных служб, каждая из которых выполняет специализированную задачу. Эти службы могут взаимодействовать друг с другом, образуя полную функцию, например для визуализации разных частей веб-приложения. Существуют также клиентские приложения, которые подключаются и обмениваются данными со службами. В этом документе описывается настройка соединения со службами в Service Fabric и между ними.

В этом видеоролике от Академии Microsoft Virtual Academy также показано взаимодействие служб: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Используйте любой удобный протокол
Service Fabric помогает управлять жизненным циклом служб, но не определяет, как они должны работать. Это относится и к обмену данными. Когда служба открывается в Service Fabric, она может настроить конечную точку для входящих запросов, используя любой протокол или стек связи. Служба будет прослушивать обычный адрес в формате **IP:порт** с использованием любой схемы адресации, например URI. Несколько экземпляров или реплик службы могут совместно использовать хост-процесс; в таком случае они должны использовать разные порты или механизм совместного использования порта, например драйвер ядра http.sys в Windows. В любом случае все экземпляры или реплики службы в хост-процессе должны быть уникально адресуемыми.

![Конечные точки службы][1]

## <a name="service-discovery-and-resolution"></a>Поиск и разрешение служб
В распределенной системе службы могут со временем быть перемещены с одного компьютера на другой. Это может происходить по разным причинам, например при балансировке, обновлении, отработке отказа или масштабировании ресурсов. Таким образом, если служба перейдет на узел с другим IP-адресом, изменится адрес ее конечной точки, а если служба использует динамически выбранный порт, то может измениться и порт.

![Распределение служб][7]

Service Fabric включает службу именования, которая позволяет находить и разрешать службы. В службе именования используется таблица для сопоставления именованных экземпляров службы с адресами, которые прослушиваются конечными точками. Все именованные экземпляры службы в Service Fabric имеют уникальные универсальные коды ресурса (URI) в качестве имен, например `"fabric:/MyApplication/MyService"`. Имя службы не изменяется на всем протяжении ее существования. При перемещении службы может измениться только адрес конечной точки. Это аналогично веб-сайтам, URL-адреса которых не меняются, даже когда могут меняться их IP-адреса. Service Fabric использует регистратор, который сопоставляет имена служб и адреса конечных точек, примерно так же, как система DNS разрешает URL-адреса в IP-адреса.

![Конечные точки службы][2]

Разрешение служб и подключение к ним состоит из следующих шагов, которые выполняются циклически.

* **Разрешение**: получение конечной точки, которая опубликована из службы именования.
* **Подключение**: подключение к службе по любому протоколу, который используется для этой конечной точки.
* **Повтор**: попытка подключения может завершиться неудачей по ряду причин, например, если служба была перемещена после предыдущего разрешения адреса ее конечной точки. В этом случае нужно повторить шаги разрешения и подключения. Этот цикл повторяется, пока подключение не будет установлено.

## <a name="connecting-to-other-services"></a>Подключение к другим службам
Службы, которые подключаются друг к другу в рамках кластера, обычно могут напрямую обратиться к конечным точкам другой службы, так как узлы в кластере расположены в пределах одной локальной сети. Чтобы упростить подключение между службами, Service Fabric предоставляет дополнительные службы, использующие службу именования: служба DNS и служба обратного прокси-сервера.


### <a name="dns-service"></a>Служба DNS
Так как многие службы, а именно контейнерные службы, могут содержать URL-адрес, возможность разрешить его с помощью стандартного протокола DNS (а не протокола службы именования) очень удобна, особенно в сценариях Lift-аnd-Shift приложения. Именно это и делает служба DNS. Она позволяет сопоставить DNS-имена с именем службы и, следовательно, разрешить IP-адреса конечных точек. 

Как показано на схеме ниже, служба DNS, выполняющаяся в кластере Service Fabric, сопоставляет DNS-имена с именами служб, которые затем разрешаются службой именования, чтобы вернуть адреса конечных точек для подключения. DNS-имя службы предоставляется при создании. 

![Конечные точки службы][9]

Дополнительные сведения об использовании службы DNS см. в статье [DNS Service in Azure Service Fabric](service-fabric-dnsservice.md) (Служба DNS в Azure Service Fabric).

### <a name="reverse-proxy-service"></a>Служба обратного прокси-сервера
Службы адресов обратного прокси-сервера находятся в кластере, предоставляющем конечные точки HTTP, включая HTTPS. Обратный прокси-сервер значительно упрощает вызов других служб и их методов за счет определенного формата URI и обрабатывает шаги разрешения, подключения и повторения, необходимые для взаимодействия между службами, с помощью службы именования. Другими словами, он скрывает службу именования при вызове других служб, что выполняется так же просто, как и вызов URL-адреса.

![Конечные точки службы][10]

Дополнительные сведения об использовании службы обратного прокси-сервера см. в статье [Обратный прокси-сервер в Azure Service Fabric](service-fabric-reverseproxy.md).

## <a name="connections-from-external-clients"></a>Подключения от внешних клиентов
Службы, которые подключаются друг к другу в рамках кластера, обычно могут напрямую обратиться к конечным точкам другой службы, так как узлы в кластере расположены в пределах одной локальной сети. Однако в некоторых средах балансировщик нагрузки, который направляет приходящий извне трафик через ограниченный набор портов, может располагаться за кластером. В таких случаях службы также могут взаимодействовать друг с другом и разрешать адреса через службу именования, но для подключения внешних клиентов потребуются дополнительные шаги.

## <a name="service-fabric-in-azure"></a>Service Fabric в Azure
Балансировщик нагрузки Azure расположен за кластером Service Fabric в Azure. Весь внешний трафик кластера должен пройти через балансировщик нагрузки. Балансировщик нагрузки будет автоматически пересылать трафик, входящий на определенный порт, к любому *узлу* , на котором открыт такой же порт. Azure Load Balancer известно только о том, какие порты открыты на каких *узлах*, но ничего не известно о том, какие *службы* их открыли.

![Топология балансировщика нагрузки и Service Fabric в Azure][3]

Например, чтобы принимать внешний трафик через порт **80**, нужно выполнить следующие настройки.

1. Создайте службу, прослушивающую порт 80. Настройте порт 80 в файле ServiceManifest.xml для этой службы и откройте в ней прослушиватель, например резидентный веб-сервер.

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
2. Создайте в Azure кластер Service Fabric и укажите в нем порт **80** как порт пользовательской конечной точки для такого типа узла, на котором будет размещена служба. Если у вас используются узлы нескольких типов, можно настроить для службы *ограничения на размещение* , чтобы она выполнялась только на том типе узла, для которого открыт порт пользовательской конечной точки.

    ![Открытие порта для типа узла][4]
3. Когда будет создан кластер, настройте балансировщик нагрузки Azure в группе ресурсов кластера, чтобы он перенаправлял трафик на порт 80. При создании кластера на портале Azure это перенаправление настраивается автоматически для каждого настроенного порта пользовательской конечной точки.

    ![Перенаправление трафика в балансировщике нагрузки Azure][5]
4. Балансировщик нагрузки Azure использует зонд для выбора узла, на который можно направлять трафик. Зонд периодически опрашивает конечную точку на каждом узле и проверяет, отвечает ли узел. Если зонд не получает ответ после определенного числа запросов, балансировщик нагрузки прекращает отправку трафика на этот узел. Когда вы создаете кластер с помощью портала Azure, зонд настраивается автоматически для каждого открытого порта пользовательской конечной точки.

    ![Перенаправление трафика в балансировщике нагрузки Azure][8]

Важно помнить, что Azure Load Balancer и зонды получают информацию только об *узлах*, но не о *службах*, которые на них запущены. Балансировщик нагрузки Azure будет отправлять трафик только на те узлы, которые отвечают на запросы зонда. Поэтому нужно внимательно следить, чтобы на узлах работали службы, которые могут отвечать на эти запросы.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services. Встроенные варианты API для обмена данными
Платформа Reliable Services доступна с несколькими вариантами интерфейсов для организации связи. Выбор оптимального варианта зависит от модели программирования, платформы взаимодействия и языка программирования, на котором написаны службы.

* **Без указания конкретного протокола**. Если у вас нет предпочтений в отношении платформы для обмена данными, а нужно просто быстро настроить и запустить какое-либо решение, идеальным вариантом будет [удаленное взаимодействие между службами](service-fabric-reliable-services-communication-remoting.md). Это позволит использовать вызовы процедур Reliable Services и Reliable Actors со строгим контролем типов. Это самый простой и наиболее быстрый способ начать обмен данными между службами. Удаленное взаимодействие между службами берет на себя разрешение адреса службы, процедуры подключения, повторных попыток и обработки ошибок. Эта возможность доступна для приложений на C# и Java.
* **HTTP**: протокол HTTP — это стандартный вариант для обмена данными между системами на любых языках. Платформа Service Fabric поддерживает любые средства для HTTP и HTTP-серверы, доступные для множества языков. Службы могут использовать любой из существующих стеков HTTP, в том числе [веб-API ASP.NET](service-fabric-reliable-services-communication-webapi.md) для приложений на C#. Клиенты, написанные на языке C#, могут использовать классы `ICommunicationClient` и `ServicePartitionClient`, а написанные на Java — классы `CommunicationClient` и `FabricServicePartitionClient`, [для разрешения адресов служб, обработки подключений HTTP и циклов повтора](service-fabric-reliable-services-communication.md).
* **WCF**: если у вас есть существующий код, который использует WCF как среду обмена данными, то вы можете использовать класс `WcfCommunicationListener` на стороне сервера и классы `WcfCommunicationClient` и `ServicePartitionClient` на стороне клиента. Но это доступно только для приложений на C# в кластерах на платформе Windows. Дополнительные сведения см. в статье [Реализация стека связи на основе WCF](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Использование пользовательских протоколов и других платформ для обмена данными
Ваши службы могут использовать для обмена данными любой протокол и любую платформу, будь то пользовательский двоичный протокол, работающий через сокеты TCP, или события потоковой передачи с использованием [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) или [Центра Интернета вещей Azure](https://azure.microsoft.com/services/iot-hub/). Service Fabric предусматривает API-интерфейсы для обмена данными, к которым можно подключить любой стек связи. При этом от вас будут скрыты все процессы, связанные с поиском служб и подключением к ним. Дополнительные сведения см. в статье [Модель взаимодействия надежных служб](service-fabric-reliable-services-communication.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о доступных понятиях и интерфейсах см. в описании [модели взаимодействия Reliable Services](service-fabric-reliable-services-communication.md). Далее вы можете быстро приступить к работе с [удаленным взаимодействием между службами](service-fabric-reliable-services-communication-remoting.md) или узнать, как создать собственный прослушиватель связи с помощью [веб-API с тестированием OWIN](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
