---
title: "aaaAzure Service Fabric обратный прокси-сервер | Документы Microsoft"
description: "Используйте toomicroservices связи с внутренней и внешней hello кластера Service Fabric обратного прокси-сервера."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="18367-103">Обратный прокси-сервер в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18367-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="18367-104">Hello обратного прокси-сервера, встроенный в Azure Service Fabric адреса микрослужбами в кластере Service Fabric hello, который предоставляет конечные точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="18367-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="18367-105">Модель взаимодействия с микрослужбами</span><span class="sxs-lookup"><span data-stu-id="18367-105">Microservices communication model</span></span>
<span data-ttu-id="18367-106">Как правило, Микрослужбами в Service Fabric работы на подмножестве виртуальных машин в кластере hello и можно перемещать из одного tooanother виртуальной машины по различным причинам.</span><span class="sxs-lookup"><span data-stu-id="18367-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="18367-107">Таким образом hello конечных точек для микрослужбами можно изменять динамически.</span><span class="sxs-lookup"><span data-stu-id="18367-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="18367-108">Hello стандартным шаблоном toocommunicate toohello микрослужбу — hello следующие решения цикла:</span><span class="sxs-lookup"><span data-stu-id="18367-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="18367-109">Разрешить размещение службы hello изначально через службу имен hello.</span><span class="sxs-lookup"><span data-stu-id="18367-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="18367-110">Подключения toohello службы.</span><span class="sxs-lookup"><span data-stu-id="18367-110">Connect toohello service.</span></span>
3. <span data-ttu-id="18367-111">Определить причину сбоев подключения hello и устраните расположение службы hello еще раз, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="18367-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="18367-112">Этот процесс обычно включает упаковки связи клиентских библиотек в цикле повтора, который реализует hello политики службы разрешения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="18367-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="18367-113">Дополнительные сведения см. в разделе [Подключение к службам в Service Fabric и взаимодействие с ними](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="18367-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="18367-114">Связь с использованием hello обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="18367-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="18367-115">Hello обратного прокси-сервера в Service Fabric запускается на всех узлах кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="18367-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="18367-116">Она выполняет процесс разрешения hello всей службы от имени клиента и затем перенаправляет запрос клиента hello.</span><span class="sxs-lookup"><span data-stu-id="18367-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="18367-117">Таким образом клиенты, работающие в кластере hello можно использовать любую клиентские HTTP связи библиотеки tootalk toohello целевую службу с помощью hello обратного прокси-сервера hello, выполняется локально на одном узле.</span><span class="sxs-lookup"><span data-stu-id="18367-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Взаимодействие изнутри][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="18367-119">Достижение микрослужбами из вне кластера hello</span><span class="sxs-lookup"><span data-stu-id="18367-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="18367-120">модель внешней связи по умолчанию Hello для микрослужбами представляет собой модель согласиться на использование, где каждая служба нельзя обращаться непосредственно из внешних клиентов.</span><span class="sxs-lookup"><span data-stu-id="18367-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="18367-121">[Подсистема балансировки нагрузки Azure](../load-balancer/load-balancer-overview.md), являющееся границы сети между микрослужбами и внешними клиентами выполняет преобразование сетевых адресов и пересылает внешние запросы конечных точек toointernal IP: Port.</span><span class="sxs-lookup"><span data-stu-id="18367-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="18367-122">toomake клиентов доступны непосредственно tooexternal микрослужбу конечной точки, необходимо сначала настроить использует порт tooeach tooforward трафика, который hello службы балансировки нагрузки в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="18367-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="18367-123">Кроме того большинство микрослужбами, особенно с отслеживанием состояния микрослужбами не live на всех узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="18367-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="18367-124">Hello микрослужбами можно перемещать между узлами при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="18367-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="18367-125">В таких случаях подсистема балансировки нагрузки не может определить эффективно hello расположение целевого узла hello toowhich реплик hello пересылать трафик.</span><span class="sxs-lookup"><span data-stu-id="18367-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="18367-126">Достижение микрослужбами через hello обратного прокси-сервера из кластера вне hello</span><span class="sxs-lookup"><span data-stu-id="18367-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="18367-127">Вместо настройки порта hello отдельных службы в подсистему балансировки нагрузки, можно настроить только hello порт hello обратного прокси-сервера в подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="18367-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="18367-128">Эта конфигурация позволяет клиентам за пределами кластера hello достичь служб внутри hello кластера с помощью hello обратный прокси-сервер без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="18367-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Взаимодействие извне][0]

> [!WARNING]
> <span data-ttu-id="18367-130">При настройке обратных прокси hello порт в подсистему балансировки нагрузки все микрослужбами hello кластера, которые предоставляют конечную точку HTTP адресуемых за пределами кластера hello.</span><span class="sxs-lookup"><span data-stu-id="18367-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="18367-131">Формат URI для адресации служб с помощью hello обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="18367-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="18367-132">Здравствуйте, использующая обратного прокси-сервера следует перенаправить конкретных универсальный код ресурса идентификатора (URI) формат tooidentify hello секции toowhich hello входящих запрос службы:</span><span class="sxs-lookup"><span data-stu-id="18367-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="18367-133">**HTTP (s):** hello обратного прокси-сервера может быть настроенный tooaccept HTTP или HTTPS-трафика.</span><span class="sxs-lookup"><span data-stu-id="18367-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="18367-134">Пересылка HTTPS можно найти слишком[подключения служба безопасного tooa обратного прокси-сервера hello](service-fabric-reverseproxy-configure-secure-communication.md) после установки toolisten обратный прокси-сервер HTTPS.</span><span class="sxs-lookup"><span data-stu-id="18367-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="18367-135">**Кластер полное доменное имя (FQDN) | внутренний IP-адрес:** для внешних клиентов можно настроить hello обратного прокси-сервера, чтобы он будет доступен через домен кластера hello, например mycluster.eastus.cloudapp.azure.com. По умолчанию hello обратный прокси-сервер работает на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="18367-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="18367-136">Для внутреннего трафика hello обратного прокси-сервера можно получить на localhost или на любой внутренний узел IP-адрес, например 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="18367-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="18367-137">**Порт:** порт hello, например 19081, который был задан для hello обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="18367-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="18367-138">**ServiceInstanceName:** hello полное имя экземпляра службы hello развернуты, что вы пытаетесь tooreach без hello «fabric: / «схемы.</span><span class="sxs-lookup"><span data-stu-id="18367-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="18367-139">Например, hello tooreach *fabric: / myapp/myservice/* службы, следует использовать *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="18367-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="18367-140">Имя экземпляра службы Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="18367-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="18367-141">С помощью другой регистр символов для имени экземпляра службы hello в URL-АДРЕСЕ hello вызывает toofail hello запросы с 404 (не найдено).</span><span class="sxs-lookup"><span data-stu-id="18367-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="18367-142">**Суффикс пути:** это фактический URL-путь hello *myapi/значения/добавить/3*, для нужной tooconnect для службы hello.</span><span class="sxs-lookup"><span data-stu-id="18367-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="18367-143">**PartitionKey:** для секционированных службы, это ключ вычисляемую секцию hello hello секции, которые должны tooreach.</span><span class="sxs-lookup"><span data-stu-id="18367-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="18367-144">Обратите внимание, что это *не* hello идентификатор GUID раздела.</span><span class="sxs-lookup"><span data-stu-id="18367-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="18367-145">Этот параметр не является обязательным для служб, использующих hello одноэлементную схему секционирования.</span><span class="sxs-lookup"><span data-stu-id="18367-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="18367-146">**PartitionKind:** это hello схемы секционирования службы.</span><span class="sxs-lookup"><span data-stu-id="18367-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="18367-147">Это может иметь значение "Int64Range" (Диапазон Int64) или "Named" (Именованная).</span><span class="sxs-lookup"><span data-stu-id="18367-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="18367-148">Этот параметр не является обязательным для служб, использующих hello одноэлементную схему секционирования.</span><span class="sxs-lookup"><span data-stu-id="18367-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="18367-149">**ListenerName** hello конечные точки из службы hello имеют форму hello {«Конечные точки»: {«Listener1»: «Endpoint1», «Listener2»: «Endpoint2»...}}.</span><span class="sxs-lookup"><span data-stu-id="18367-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="18367-150">Когда hello служба предоставляет несколько конечных точек, определяет конечную точку hello, запрос клиента hello должен быть передан.</span><span class="sxs-lookup"><span data-stu-id="18367-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="18367-151">Это можно опустить, если служба hello имеется только один прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="18367-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="18367-152">**TargetReplicaSelector** указывает, каким образом должен быть выбран hello целевая реплика или экземпляр.</span><span class="sxs-lookup"><span data-stu-id="18367-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="18367-153">Когда hello целевой службы с отслеживанием состояния, hello TargetReplicaSelector может принимать одно из следующих hello: «PrimaryReplica», «RandomSecondaryReplica» или «RandomReplica».</span><span class="sxs-lookup"><span data-stu-id="18367-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="18367-154">Если этот параметр не указан, по умолчанию hello — «PrimaryReplica».</span><span class="sxs-lookup"><span data-stu-id="18367-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="18367-155">При hello целевой службы без сохранения состояния, обратный прокси-сервер принимает экземпляр случайных hello секции tooforward hello запрос службы.</span><span class="sxs-lookup"><span data-stu-id="18367-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="18367-156">**Время ожидания:** указывает hello время ожидания для запроса hello HTTP, созданные службы toohello hello обратный прокси-сервер от имени hello клиентского запроса.</span><span class="sxs-lookup"><span data-stu-id="18367-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="18367-157">значение по умолчанию Hello составляет 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="18367-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="18367-158">Данный параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="18367-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="18367-159">Пример использования</span><span class="sxs-lookup"><span data-stu-id="18367-159">Example usage</span></span>
<span data-ttu-id="18367-160">В качестве примера рассмотрим hello *fabric: / MyApp/MyService* службу, которая открывает прослушиватель HTTP на hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="18367-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="18367-161">Ниже приведены ресурсы hello hello службы:</span><span class="sxs-lookup"><span data-stu-id="18367-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="18367-162">Если служба hello использует схему секционирования singleton hello, hello *PartitionKey* и *PartitionKind* параметры строки запроса не являются обязательными, а hello службы можно получить с помощью шлюза hello как:</span><span class="sxs-lookup"><span data-stu-id="18367-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="18367-163">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="18367-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="18367-164">Изнутри: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="18367-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="18367-165">Если служба hello использует hello универсальный Int64 схему секционирования, hello *PartitionKey* и *PartitionKind* параметры строки запроса должен быть используется tooreach секции hello службы:</span><span class="sxs-lookup"><span data-stu-id="18367-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="18367-166">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="18367-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="18367-167">Изнутри: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="18367-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="18367-168">tooreach hello ресурсов, предоставляемых службой hello, просто поместите hello пути к ресурсу после имени службы hello в hello URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="18367-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="18367-169">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="18367-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="18367-170">Изнутри: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="18367-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="18367-171">шлюз Hello затем будет пересылать toohello службы эти запросы на URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="18367-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="18367-172">Специальные действия для служб с общим доступом к портам</span><span class="sxs-lookup"><span data-stu-id="18367-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="18367-173">Шлюз Azure приложение пытается tooresolve службы адрес еще раз и повторите запрос hello в том случае, когда службы невозможен.</span><span class="sxs-lookup"><span data-stu-id="18367-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="18367-174">Это Главное преимущество шлюза приложения, так как клиентский код не требуется tooimplement свои собственные разрешения для службы и разрешать цикла.</span><span class="sxs-lookup"><span data-stu-id="18367-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="18367-175">Как правило когда службы невозможен, экземпляр службы hello или реплики перемещено tooa другой узел в рамках своего обычного жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="18367-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="18367-176">В этом случае шлюз приложений может получать сети подключения ошибки указывает, что конечной точки, что нет открытых больше времени на hello изначально разрешить адрес.</span><span class="sxs-lookup"><span data-stu-id="18367-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="18367-177">Тем не менее реплики или экземпляры службы могут совместно использовать хост-процесс и даже порт при размещении на веб-сервере на основе http.sys, включая:</span><span class="sxs-lookup"><span data-stu-id="18367-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="18367-178">System.Net.HttpListener;</span><span class="sxs-lookup"><span data-stu-id="18367-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="18367-179">ASP.NET Core WebListener;</span><span class="sxs-lookup"><span data-stu-id="18367-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="18367-180">Katana.</span><span class="sxs-lookup"><span data-stu-id="18367-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="18367-181">В этом случае вполне вероятно, hello веб-сервер доступен в хост-процесса hello и отвечать на запросы toorequests, но hello разрешении экземпляр службы или реплика больше не доступен на узле hello.</span><span class="sxs-lookup"><span data-stu-id="18367-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="18367-182">В этом случае шлюз hello получать ответы HTTP 404 hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="18367-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="18367-183">Следовательно, ошибка "HTTP 404" может иметь два разных значения.</span><span class="sxs-lookup"><span data-stu-id="18367-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="18367-184">#1: адрес службы hello имеют правильный регистр, но ресурс hello, hello запрошенного пользователя не существует.</span><span class="sxs-lookup"><span data-stu-id="18367-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="18367-185">Случай #2: неверный адрес службы hello и ресурса hello, hello запрошенного пользователя могут существовать на другом узле.</span><span class="sxs-lookup"><span data-stu-id="18367-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="18367-186">Hello первый случай — обычный HTTP 404, который считается пользовательской ошибки.</span><span class="sxs-lookup"><span data-stu-id="18367-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="18367-187">Однако в случае второй hello hello пользователь запросил ресурс, который существует.</span><span class="sxs-lookup"><span data-stu-id="18367-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="18367-188">Шлюз приложений было невозможно toolocate, он перемещен, так как hello самой службы.</span><span class="sxs-lookup"><span data-stu-id="18367-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="18367-189">Приложения требованиям tooresolve hello адрес шлюза снова и повторите попытку hello запрос.</span><span class="sxs-lookup"><span data-stu-id="18367-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="18367-190">Таким образом, использование шлюза приложений должна toodistinguish способом между этих двух случаях.</span><span class="sxs-lookup"><span data-stu-id="18367-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="18367-191">toomake, что различие, подсказку с сервера hello необходим.</span><span class="sxs-lookup"><span data-stu-id="18367-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="18367-192">По умолчанию шлюз приложений предполагает случай #2 и пытается tooresolve и проблемы hello запрос еще раз.</span><span class="sxs-lookup"><span data-stu-id="18367-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="18367-193">tooApplication вариант #1 tooindicate шлюза, hello службы должна возвращать hello, выполнив HTTP-заголовок ответа:</span><span class="sxs-lookup"><span data-stu-id="18367-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="18367-194">Этот заголовок ответа HTTP указывает на обычный HTTP 404 ситуацию, в которой hello запрошенный ресурс не существует, а шлюз приложений не будет адрес службы hello tooresolve еще раз.</span><span class="sxs-lookup"><span data-stu-id="18367-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="18367-195">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="18367-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="18367-196">Включение обратного прокси-сервера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="18367-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="18367-197">Портал Azure предоставляет параметр tooenable обратного прокси-сервера при создании нового кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="18367-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="18367-198">В разделе **кластера Service Fabric создать**, шаг 2: конфигурация кластера, конфигурация типа узла, установите флажок hello слишком «Enable обратного прокси».</span><span class="sxs-lookup"><span data-stu-id="18367-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="18367-199">Для настройки безопасного обратного прокси-сервера, SSL-сертификат может быть указано в шаге 3: слишком безопасности, Настройка параметров безопасности кластера, а также hello, установите флажок «Включить SSL-сертификат для обратного прокси-сервера» и введите сведения о сертификате hello.</span><span class="sxs-lookup"><span data-stu-id="18367-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="18367-200">Включение обратного прокси-сервера с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="18367-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="18367-201">Можно использовать hello [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello обратного прокси-сервера в Service Fabric для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="18367-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="18367-202">См. слишком[Настройка HTTPS обратного прокси-сервера в кластере безопасного](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) для диспетчера ресурсов Azure шаблона образцы tooconfigure безопасного обратного прокси-сервера с помощью сертификата и обработка смены сертификата.</span><span class="sxs-lookup"><span data-stu-id="18367-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="18367-203">Во-первых вы получаете шаблона hello hello кластера, которые должны toodeploy.</span><span class="sxs-lookup"><span data-stu-id="18367-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="18367-204">Можно использовать шаблоны образец hello или создать настраиваемый шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="18367-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="18367-205">Затем можно включить hello обратного прокси-сервера с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="18367-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="18367-206">Определить порт для hello обратного прокси-сервера в hello [раздела параметров](../azure-resource-manager/resource-group-authoring-templates.md) hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="18367-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="18367-207">Укажите порт hello для каждого из объектов nodetype hello в hello **кластера** [разделе типа ресурсов](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="18367-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="18367-208">порт Hello определяется по имени параметра hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="18367-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="18367-209">tooaddress hello обратного прокси-сервера из внешней hello Azure кластера задавать правила балансировки нагрузки Azure hello hello порт, указанный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="18367-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="18367-210">tooconfigure сертификаты SSL для порта hello для обратного прокси hello, добавьте hello сертификат toohello ***reverseProxyCertificate*** свойство в hello **кластера** [разделе типа ресурсов](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="18367-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="18367-211">Поддержка сертификат обратного прокси-сервера, который не совпадает с сертификатом hello кластера</span><span class="sxs-lookup"><span data-stu-id="18367-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="18367-212">Если сертификат hello обратного прокси-сервера не совпадает с hello сертификата, который защищает hello кластера, затем hello ранее указанный сертификат должен быть установлен на виртуальной машине hello и добавлены toohello список управления доступом (ACL), позволяющую Service Fabric доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="18367-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="18367-213">Это можно сделать в hello **virtualMachineScaleSets** [разделе типа ресурсов](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="18367-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="18367-214">Для установки добавьте osProfile toohello этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="18367-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="18367-215">раздел расширения Hello hello шаблона можно обновить сертификат hello в hello ACL.</span><span class="sxs-lookup"><span data-stu-id="18367-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="18367-216">При использовании сертификатов, которые отличаются от hello кластера сертификат tooenable hello обратного прокси-сервера в существующем кластере, установить сертификат hello обратного прокси-сервера и обновить hello ACL в кластере hello, перед включением hello обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="18367-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="18367-217">Полный hello [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) развертывания с помощью параметров hello, описанных ранее перед началом развертывания tooenable hello обратного прокси-сервера в шагах 1 – 4.</span><span class="sxs-lookup"><span data-stu-id="18367-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18367-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18367-218">Next steps</span></span>
* <span data-ttu-id="18367-219">Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="18367-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="18367-220">Служба HTTP toosecure перенаправления с hello обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="18367-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="18367-221">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="18367-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="18367-222">Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="18367-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="18367-223">Коммуникационный стек WCF для надежных служб</span><span class="sxs-lookup"><span data-stu-id="18367-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="18367-224">Дополнительные параметры конфигурации обратного прокси-сервера описаны в разделе о ApplicationGateway/Http статьи [Настройка параметров кластера Service Fabric и политики обновления структур](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="18367-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
