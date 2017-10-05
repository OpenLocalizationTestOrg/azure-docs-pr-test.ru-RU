---
title: "Обратный прокси-сервер Azure Service Fabric | Документация Майкрософт"
description: "Использование обратного прокси-сервера Service Fabric для взаимодействия с микрослужбами изнутри и извне кластера."
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
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="1ef4f-103">Обратный прокси-сервер в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1ef4f-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="1ef4f-104">Обратный прокси-сервер, встроенный в Azure Service Fabric, обслуживает микрослужбы в кластере Service Fabric, которые предоставляют конечные точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="1ef4f-105">Модель взаимодействия с микрослужбами</span><span class="sxs-lookup"><span data-stu-id="1ef4f-105">Microservices communication model</span></span>
<span data-ttu-id="1ef4f-106">Микрослужбы в Service Fabric обычно выполняются на подмножестве виртуальных машин в кластере и по различным причинам могут перемещаться с одной виртуальной машины на другую.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="1ef4f-107">Поэтому конечные точки для микрослужб могут динамически изменяться.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="1ef4f-108">Типичной схемой взаимодействия с микрослужбой является цикл разрешения, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="1ef4f-109">Первоначальное разрешение расположения службы через службу именования.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="1ef4f-110">Подключение к службе.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-110">Connect to the service.</span></span>
3. <span data-ttu-id="1ef4f-111">Определение причины ошибки подключения и при необходимости повторное разрешение расположения службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="1ef4f-112">Этот процесс обычно включает в себя заключение в оболочку клиентских библиотек связи в цикле повтора, реализующих политики разрешения службы и повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="1ef4f-113">Дополнительные сведения см. в разделе [Подключение к службам в Service Fabric и взаимодействие с ними](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="1ef4f-114">Обмен данными с использованием обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="1ef4f-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="1ef4f-115">Обратный прокси-сервер Service Fabric запускается на всех узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="1ef4f-116">Он выполняет весь процесс разрешения службы от имени клиента, а затем пересылает запрос клиента.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="1ef4f-117">Поэтому клиенты, работающие в кластере, могут использовать любые клиентские библиотеки связи HTTP взаимодействия с целевой службой через обратный прокси-сервер, который выполняется локально на том же узле.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![Взаимодействие изнутри][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="1ef4f-119">Обращение к микрослужбам извне кластера</span><span class="sxs-lookup"><span data-stu-id="1ef4f-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="1ef4f-120">По умолчанию микрослужбы для внешнего взаимодействия используют модель участия: к любой службе нельзя получить доступ напрямую из внешних клиентов.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="1ef4f-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md) — это граница сети между микрослужбами и внешними клиентами, которая выполняет преобразование сетевых адресов и пересылает внешние запросы к внутренним конечным точкам "IP-адрес:порт".</span><span class="sxs-lookup"><span data-stu-id="1ef4f-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="1ef4f-122">Чтобы внешние клиенты могли напрямую обращаться к конечной точке, нужно сначала настроить подсистему балансировки нагрузки для пересылки трафика каждого порта, используемого службой в кластере.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="1ef4f-123">Более того, большая часть микрослужб, особенно микрослужбы с отслеживанием состояния, не выполняется на всех узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="1ef4f-124">Микрослужбы могут перемещаться между узлами при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="1ef4f-125">В таких случаях подсистема балансировки нагрузки не может эффективно определить расположение целевого узла реплик, к которым следует пересылать трафик.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="1ef4f-126">Обращение к микрослужбам через обратный прокси-сервер извне кластера</span><span class="sxs-lookup"><span data-stu-id="1ef4f-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="1ef4f-127">Вместо того, чтобы настраивать порт отдельной службы в подсистеме балансировки нагрузки, в ней можно настроить порт обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="1ef4f-128">Такая конфигурация позволит клиентам, расположенным за пределами кластера, обращаться к службам внутри него через обратный прокси-сервер без дополнительных настроек.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![Взаимодействие извне][0]

> [!WARNING]
> <span data-ttu-id="1ef4f-130">Настройка порта обратного прокси-сервера в подсистеме балансировки нагрузки обеспечит адресацию извне кластера всех микрослужб в этом кластере, которые предоставляют конечную точку HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="1ef4f-131">Формат универсального кода ресурса (URI) для адресации служб через обратный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1ef4f-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="1ef4f-132">Обратный прокси-сервер использует определенный формат универсального кода ресурса (URI), чтобы определять, в какую секцию службы следует перенаправить входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="1ef4f-133">**http(s).** Обратный прокси-сервер можно настроить для приема трафика HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="1ef4f-134">После настройки обратного прокси-сервера для прослушивания по протоколу HTTPS ознакомьтесь со сведениями о переадресации HTTPS в статье [Подключение к безопасной службе с помощью обратного прокси-сервера](service-fabric-reverseproxy-configure-secure-communication.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="1ef4f-135">**Cluster FQDN | internal IP.** Для внешних клиентов обратный прокси-сервер можно настроить таким образом, чтобы он был доступен через домен кластера (например, mycluster.eastus.cloudapp.azure.com). По умолчанию обратный прокси-сервер выполняется на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="1ef4f-136">Для внутреннего трафика он может быть доступен на узле localhost или по IP-адресу любого внутреннего узла (например, 10.0.0.1).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="1ef4f-137">**Port.** Порт, например 19081, указанный для обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="1ef4f-138">**ServiceInstanceName.** Полное имя развернутого экземпляра службы, к которому вы пытаетесь получить доступ, без использования схемы fabric:/.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="1ef4f-139">Например, чтобы подключиться к службе *fabric:/myapp/myservice/*, используется имя *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="1ef4f-140">В имени экземпляра службы учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="1ef4f-141">Использование символов разного регистра в имени экземпляра службы в URL-адресе приводит к сбою запросов с ошибкой "404 (не найдено)".</span><span class="sxs-lookup"><span data-stu-id="1ef4f-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="1ef4f-142">**Suffix path**. Фактический URL-адрес службы, к которой вы подключаетесь, например *myapi/values/add/3*.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="1ef4f-143">**PartitionKey.** Для секционированной службы это вычисляемый ключ секции, к которой вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="1ef4f-144">Обратите внимание, что это *не* идентификатор GUID секции.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="1ef4f-145">Этот параметр не является обязательным для служб, использующих схему одноэлементного секционирования.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="1ef4f-146">**PartitionKind.** Схема секционирования службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="1ef4f-147">Это может иметь значение "Int64Range" (Диапазон Int64) или "Named" (Именованная).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="1ef4f-148">Этот параметр не является обязательным для служб, использующих схему одноэлементного секционирования.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="1ef4f-149">**ListenerName.** Конечные точки, представляемые службой, имеют следующий вид: {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}</span><span class="sxs-lookup"><span data-stu-id="1ef4f-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="1ef4f-150">Если служба представляет несколько конечных точек, то данный параметр определяет, к которой из них следует перенаправить клиентский запрос.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="1ef4f-151">При наличии только одного прослушивателя потребность в данном параметре отсутствует.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="1ef4f-152">**TargetReplicaSelector.** Данный параметр определяет, каким образом должна быть выбрана целевая реплика или экземпляр.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="1ef4f-153">Если целевая служба является службой с отслеживанием состояния, то параметр TargetReplicaSelector может иметь значение PrimaryReplica, RandomSecondaryReplica или RandomReplica.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="1ef4f-154">Если этот параметр не указан, по умолчанию используется значение PrimaryReplica.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="1ef4f-155">Если целевая служба является службой без отслеживания состояния, обратный прокси-сервер выбирает случайный экземпляр раздела службы, к которому направляется запрос.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="1ef4f-156">**Timeout.** Время ожидания HTTP-запроса к службе, созданного обратным прокси-сервером от имени клиентского запроса.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="1ef4f-157">Значение по умолчанию составляет 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-157">The default value is 60 seconds.</span></span> <span data-ttu-id="1ef4f-158">Данный параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="1ef4f-159">Пример использования</span><span class="sxs-lookup"><span data-stu-id="1ef4f-159">Example usage</span></span>
<span data-ttu-id="1ef4f-160">Для примера рассмотрим службу *fabric:/MyApp/MyService*, которая открывает прослушиватель HTTP по приведенному ниже URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="1ef4f-161">Ниже приведены ресурсы для службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="1ef4f-162">Если служба использует схему одноэлементного секционирования, то параметры строки запроса *PartitionKey* и *PartitionKind* можно не указывать и к службе можно обратиться через шлюз следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="1ef4f-163">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="1ef4f-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="1ef4f-164">Изнутри: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="1ef4f-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="1ef4f-165">Если служба использует схему секционирования Uniform Int64, для обращения к секции службы необходимо использовать параметры строки запроса *PartitionKey* и *PartitionKind*.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="1ef4f-166">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="1ef4f-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="1ef4f-167">Изнутри: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="1ef4f-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="1ef4f-168">Укажите путь к ресурсу после имени службы в URL-адресе, чтобы обратиться к предоставленным службой ресурсам.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="1ef4f-169">Извне: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="1ef4f-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="1ef4f-170">Изнутри: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="1ef4f-171">Затем шлюз перешлет эти запросы по URL-адресу службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="1ef4f-172">Специальные действия для служб с общим доступом к портам</span><span class="sxs-lookup"><span data-stu-id="1ef4f-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="1ef4f-173">Шлюз приложений Azure пытается повторно разрешить адрес службы и повторить запрос, если служба недоступна.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="1ef4f-174">Это одно из основных преимуществ шлюза приложений, так как в коде клиента не требуется реализовывать собственный цикл разрешения службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="1ef4f-175">Как правило, недоступность службы означает, что экземпляр или реплика службы была перемещена на другой узел в ходе обычного жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="1ef4f-176">В этом случае шлюз приложений может получить ошибку сетевого подключения, указывающую, что конечная точка больше не открыта по первоначально разрешенному адресу.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="1ef4f-177">Тем не менее реплики или экземпляры службы могут совместно использовать хост-процесс и даже порт при размещении на веб-сервере на основе http.sys, включая:</span><span class="sxs-lookup"><span data-stu-id="1ef4f-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="1ef4f-178">System.Net.HttpListener;</span><span class="sxs-lookup"><span data-stu-id="1ef4f-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="1ef4f-179">ASP.NET Core WebListener;</span><span class="sxs-lookup"><span data-stu-id="1ef4f-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="1ef4f-180">Katana.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="1ef4f-181">В этом случае вполне вероятно, что веб-сервер доступен в хост-процессе и отвечает на запросы, но разрешенный экземпляр или реплика службы больше не доступна на узле.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="1ef4f-182">В этом случае шлюз получит от веб-сервера ответ "HTTP 404".</span><span class="sxs-lookup"><span data-stu-id="1ef4f-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="1ef4f-183">Следовательно, ошибка "HTTP 404" может иметь два разных значения.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="1ef4f-184">Случай № 1. Адрес службы указан правильно, но запрошенный пользователем ресурс не существует.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="1ef4f-185">Случай № 2. Адрес службы указан неправильно, а запрошенный пользователем ресурс может существовать на другом узле.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="1ef4f-186">В первом случае это обычная ошибка "HTTP 404", которая считается ошибкой пользователя.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="1ef4f-187">Однако во втором случае пользователь запросил ресурс, который существует.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="1ef4f-188">Шлюзу приложений не удалось найти его, так как была перемещена сама служба.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="1ef4f-189">Шлюзу приложений необходимо еще раз разрешить адрес и повторить запрос.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="1ef4f-190">Следовательно, шлюзу приложений необходим способ, позволяющий различать эти два случая.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="1ef4f-191">Для этого требуется указание от сервера.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="1ef4f-192">По умолчанию шлюз приложений предполагает, что произошел второй случай, и пытается повторить разрешение адреса службы и отправку запроса.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="1ef4f-193">Чтобы указать шлюзу приложений, что это первый случай, служба должна вернуть приведенный ниже заголовок ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="1ef4f-194">Этот заголовок ответа HTTP указывает обычную ситуацию возникновения ошибки "HTTP 404", в которой запрошенный ресурс не существует, и шлюз приложений не будет пытаться повторно разрешить адрес службы.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="1ef4f-195">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="1ef4f-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="1ef4f-196">Включение обратного прокси-сервера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="1ef4f-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="1ef4f-197">Во время создания нового кластера Service Fabric на портале Azure можно включить обратный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="1ef4f-198">Во время **создания кластера Service Fabric** на шаге 2 ("Конфигурация кластера" > "Конфигурация типа узла") установите флажок возле параметра "Включить обратный прокси-сервер".</span><span class="sxs-lookup"><span data-stu-id="1ef4f-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="1ef4f-199">Для настройки безопасного обратного прокси-сервера можно указать SSL-сертификат на шаге 3 ("Безопасность" > "Настройка параметров безопасности кластера"): установите флажок возле параметра "Включить SSL-сертификат для обратного прокси-сервера" и введите сведения о сертификате.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="1ef4f-200">Включение обратного прокси-сервера с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ef4f-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="1ef4f-201">Обратный прокси-сервер можно включить для кластера в Service Fabric с помощью [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="1ef4f-202">В статье [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) (Настройка обратного прокси-сервера HTTPS в защищенном кластере) приведены примеры шаблонов Azure Resource Manager для настройки защищенного обратного прокси-сервера с сертификатом и обработки смены сертификатов.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="1ef4f-203">Сначала следует получить шаблон для кластера, который требуется развернуть.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="1ef4f-204">Можно использовать примеры шаблонов или создать пользовательский шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="1ef4f-205">Затем можно включить обратный прокси-сервер, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="1ef4f-206">Определите порт обратного прокси-сервера в разделе [Parameters](../azure-resource-manager/resource-group-authoring-templates.md) шаблона.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="1ef4f-207">Укажите порт для каждого типа узлов в подразделе [Cluster](../azure-resource-manager/resource-group-authoring-templates.md) **раздела типов ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="1ef4f-208">Порт идентифицируется по имени параметра reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="1ef4f-209">Для обращения к обратному прокси-серверу извне кластера Azure настройте правила Azure Load Balancer для порта, указанного на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="1ef4f-210">Чтобы настроить SSL-сертификаты для порта обратного прокси-сервера, добавьте сертификат в свойство ***reverseProxyCertificate*** в подразделе **Cluster** [раздела типов ресурсов](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="1ef4f-211">Поддержка сертификата обратного прокси-сервера, отличного от сертификата кластера</span><span class="sxs-lookup"><span data-stu-id="1ef4f-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="1ef4f-212">Если сертификат обратного прокси-сервера отличается от сертификата, который защищает кластер, то указанный ранее сертификат необходимо установить на виртуальную машину и добавить в список управления доступом (ACL), чтобы предоставить Service Fabric к нему доступ.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="1ef4f-213">Для этого вы можете использовать **virtualMachineScaleSets** в [разделе типов ресурсов](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="1ef4f-214">Чтобы установить сертификат, добавьте его в osProfile.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="1ef4f-215">Раздел extension шаблона позволяет обновить сертификат в списке управления доступом.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-215">The extension section of the template can update the certificate in the ACL.</span></span>

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
> <span data-ttu-id="1ef4f-216">Чтобы в существующем кластере включить обратный прокси-сервер с сертификатом, отличающимся от сертификата кластера, необходимо сначала установить сертификат обратного прокси-сервера и обновить список управления доступом в кластере.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="1ef4f-217">Выполните развертывание [шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), используя описанные выше параметры, прежде чем начинать развертывание для включения обратного прокси-сервера с помощью шагов 1–4.</span><span class="sxs-lookup"><span data-stu-id="1ef4f-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ef4f-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ef4f-218">Next steps</span></span>
* <span data-ttu-id="1ef4f-219">Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="1ef4f-220">Подключение к безопасной службе с помощью обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="1ef4f-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="1ef4f-221">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1ef4f-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="1ef4f-222">Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="1ef4f-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="1ef4f-223">Коммуникационный стек WCF для надежных служб</span><span class="sxs-lookup"><span data-stu-id="1ef4f-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="1ef4f-224">Дополнительные параметры конфигурации обратного прокси-сервера описаны в разделе о ApplicationGateway/Http статьи [Настройка параметров кластера Service Fabric и политики обновления структур](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1ef4f-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
